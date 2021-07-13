<template>
  <div class="logout"></div>
</template>

<script>
import axios from "axios";
export default {
  created: function () {
    delete axios.defaults.headers.common["Authorization"];
    localStorage.removeItem("twitch_access_token");
    this.$router.push("/");
    console.log("You have been logged out, Thanks for stopping by! ");
  },
};
</script>
