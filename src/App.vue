<template>
  <div id="app">
    <nav-bar></nav-bar>
    <router-view />
  </div>
</template>

<style>
html body {
  background-color: #6f42c1;
}
</style>
<script>
import NavBar from "@/components/NavBar.vue";
export default {
  name: "nav",
  components: { "nav-bar": NavBar },
};
</script>
