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

export default {
  data() {
    return {
      type: "",
      text: [],
      loading: true,
      error: ""
    };
  },
  mounted() {
    axios
      .get("https://cat-fact.herokuapp.com/facts")
      .then((response) => {
        this.type = response.data[1].type;
        this.text = response.data[1].text;
        this.loading = false;
      })
      .catch((error) => {
        this.error = error.message;
        this.loading = false;
      });
  }
};
</script>
