<template>
  <div id="app">
    <nav-bar></nav-bar>
    <router-view />
  </div>
</template>

<style></style>
<script>
import NavBar from "@/components/NavBar.vue";
export default {
  name: "nav",
  components: { "nav-bar": NavBar },
};
</script>
