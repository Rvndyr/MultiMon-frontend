<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light" style="background-color: #3b3b44">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Twitch Multi-Mon</a>
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

        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <router-link class="nav-link active" aria-current="page" to="/">Home</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="About">About</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="Login">Login</router-link>
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
export default {};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
a {
  color: #fff !important;
  font-weight: 500;
}
</style>
