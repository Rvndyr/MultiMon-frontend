<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light" style="background-color: #3b3b44">
      <div class="container-fluid">
        <router-link class="navbar-brand navBrand" to="/">Multi-Mon</router-link>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse navFont" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <router-link class="nav-link active" aria-current="page" to="/">Home</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="About">About</router-link>
            </li>
            <li class="nav-item" v-if="!isLoggedIn()">
              <router-link class="nav-link" to="Login">Login</router-link>
            </li>
            <li class="nav-item" v-if="isLoggedIn()">
              <router-link class="nav-link" to="Logout">Logout</router-link>
            </li>
          </ul>
          <!-- Search function not yet impletmented -->
          <!-- <form class="d-flex">
            <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search" />
            <button class="btn btn-secondary" type="submit">Search</button>
          </form> -->
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
export default {
  methods: {
    isLoggedIn: function () {
      return localStorage.getItem("twitch_access_token");
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap");
a {
  color: #fff !important;
  font-weight: 500;
}
.navBrand {
  font-family: "Press Start 2P", cursive;
}
.navFont {
  font-family: "Encode Sans SC", sans-serif;
}
</style>
