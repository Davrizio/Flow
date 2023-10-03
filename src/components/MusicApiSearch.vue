<template>
  <div class="">
    <img :src="image" alt="artist image" />
  </div>
</template>

<script>
import axios from "axios";
const headers = {
  "User-Agent": "My Artist Search/1.0",
  Authorization:
    "Discogs key=YJtvkuqAEXCJOqmrEPCD, secret=dAKxsegtWuaMqsOOZpxlFvzizKbYPBox"
};
export default {
  data() {
    return {
      image: "",
      id: "",
      loading: true,
      error: ""
    };
  },
  mounted() {
    axios
      .get("https://api.discogs.com//database/search?q={nirvana}&{?artist}", {
        headers
      })
      .then((response) => {
        this.image = response.data.results[0].cover_image;
        this.id = response.data.results[0].id;
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
