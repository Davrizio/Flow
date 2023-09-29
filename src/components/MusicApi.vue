<template>
  <div class="text-white text-base">
    <h1>{{ type }}</h1>
    <h1>{{ text }}</h1>
    <ul v-if="loading">
      <li>Loading...</li>
    </ul>
    <ul v-else-if="error">
      <li>Error: {{ error }}</li>
    </ul>
    <ul v-else>
      <li v-for="item in text" :key="item.id">{{ item.name }}</li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
const headers = {
  "User-Agent": "My Artist Search/1.0"
};

export default {
  data() {
    return {
      type: "",
      text: "",
      loading: true,
      error: ""
    };
  },
  mounted() {
    axios
      .get("https://api.discogs.com/releases/249504", {
        headers
      })
      .then((response) => {
        this.type = response.data.artists[0].idArtist;
        this.text = response.data.artists[0].strArtist;
        this.loading = false;
        console.log(response);
      })
      .catch((error) => {
        this.error = error.message;
        this.loading = false;
      });
  }
};
</script>
