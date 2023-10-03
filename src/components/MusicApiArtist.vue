<template>
  <div class="text-white text-base">
    <md-block>{{ bio }}</md-block>
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
      bio: "",
      yearsActive: "",
      loading: true,
      error: ""
    };
  },
  mounted() {
    axios
      .get("https://api.discogs.com/artists/125246", {
        headers
      })
      .then((response) => {
        this.bio = response.data.profile;
        this.yearsActive = response.profile;
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
