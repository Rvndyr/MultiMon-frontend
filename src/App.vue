<template>
  <div id="app">
    <nav-bar v-if="!['Login'].includes($route.name)"></nav-bar>

    <router-view />
  </div>
</template>

<style>
html body {
  background: linear-gradient(to right, rgb(142, 45, 226), rgb(74, 0, 224));
}
</style>
<script>
import NavBar from "@/components/NavBar.vue";
export default {
  name: "nav",
  components: { "nav-bar": NavBar },
};
</script>
