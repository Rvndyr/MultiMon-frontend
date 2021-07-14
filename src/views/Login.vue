<template>
  <div>
    <!-- Header -->
    <div class="header bg-gradient-success py-7 py-lg-8 pt-lg-9">
      <b-container>
        <div class="header-body text-center mb-7">
          <b-row class="justify-content-center">
            <b-col xl="5" lg="6" md="8" class="px-5">
              <h1 class="text-white">Welcome!</h1>
              <p class="text-lead text-white">
                Use the Twitch button below to login through Twitch and get access to your followers
              </p>
            </b-col>
          </b-row>
        </div>
      </b-container>
      <div class="separator separator-bottom separator-skew zindex-100">
        <svg
          x="0"
          y="0"
          viewBox="0 0 2560 100"
          preserveAspectRatio="none"
          version="1.1"
          xmlns="http://www.w3.org/2000/svg"
        >
          <polygon class="fill-default" points="2560 0 2560 100 0 100"></polygon>
        </svg>
      </div>
    </div>
    <!-- Page content -->
    <b-container class="mt--8 pb-5">
      <b-row class="justify-content-center">
        <b-col lg="5" md="7">
          <b-card no-body class="bg-trasparant border-0 mb-0">
            <b-card-header class="bg-transparant pb-5">
              <div class="text-muted text-center mt-2 mb-3"><small>Sign in with</small></div>
              <div class="btn-wrapper text-center">
                <a
                  href="https://id.twitch.tv/oauth2/authorize?client_id=eliq1ssshmd7dc0z0ohal5zz8pszlc&redirect_uri=http://localhost:8080&response_type=code&scope=user:read:email%20user:read:follows"
                  class="btn btn-neutral btn-icon"
                >
                  <span class="btn-inner--icon">
                    <img src="https://img.icons8.com/color/48/000000/twitch--v2.png" />
                  </span>
                  <span class="btn-inner--text">Twitch</span>
                </a>
              </div>
            </b-card-header>
          </b-card>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>
<style>
.header {
  position: relative;
}
.bg-gradient-success {
  background: linear-gradient(87deg, #6c757d, #6c757d) !important;
}
.fill-default {
  fill: #6c757d;
}
*,
:after,
:before {
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}
user agent stylesheet :not(svg) {
  transform-origin: 0px 0px;
}
.col,
.col-1,
.col-2,
.col-3,
.col-4,
.col-5,
.col-6,
.col-7,
.col-8,
.col-9,
.col-10,
.col-11,
.col-12,
.col-auto,
.col-lg,
.col-lg-1,
.col-lg-2,
.col-lg-3,
.col-lg-4,
.col-lg-5,
.col-lg-6,
.col-lg-7,
.col-lg-8,
.col-lg-9,
.col-lg-10,
.col-lg-11,
.col-lg-12,
.col-lg-auto,
.col-md,
.col-md-1,
.col-md-2,
.col-md-3,
.col-md-4,
.col-md-5,
.col-md-6,
.col-md-7,
.col-md-8,
.col-md-9,
.col-md-10,
.col-md-11,
.col-md-12,
.col-md-auto,
.col-sm,
.col-sm-1,
.col-sm-2,
.col-sm-3,
.col-sm-4,
.col-sm-5,
.col-sm-6,
.col-sm-7,
.col-sm-8,
.col-sm-9,
.col-sm-10,
.col-sm-11,
.col-sm-12,
.col-sm-auto,
.col-xl,
.col-xl-1,
.col-xl-2,
.col-xl-3,
.col-xl-4,
.col-xl-5,
.col-xl-6,
.col-xl-7,
.col-xl-8,
.col-xl-9,
.col-xl-10,
.col-xl-11,
.col-xl-12,
.col-xl-auto {
  position: relative;
  width: 100%;
  padding-right: 15px;
  padding-left: 15px;
}
*,
:after,
:before {
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}
.mb-0,
.my-0 {
  margin-bottom: 0 !important;
}
.border-0 {
  border: 0 !important;
}
.bg-secondary {
  background-color: #f7fafc !important;
}
.card {
  position: relative;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -ms-flex-direction: column;
  flex-direction: column;
  min-width: 0;
  word-wrap: break-word;
  background-color: #fff;
  background-clip: border-box;
  border: 1px solid rgba(0, 0, 0, 0.05);
  border-radius: 0.375rem;
}
*,
:after,
:before {
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}
.text-center {
  text-align: center !important;
}
*,
:after,
:before {
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}
.card {
  background-color: #f7fafc !important;
}
.btn:not(:last-child) {
  margin-right: 0.5rem;
}
.btn-neutral,
.btn-neutral:hover {
  color: #212529;
  background-color: #fff;
  border-color: #fff;
}
.btn {
  position: relative;
  text-transform: none;
  -webkit-transition: all 0.15s ease;
  transition: all 0.15s ease;
  letter-spacing: 0.025em;
  font-size: 0.875rem;
  will-change: transform;
}
.btn-neutral {
  -webkit-box-shadow: 0 4px 6px rgb(50 50 93 / 11%), 0 1px 3px rgb(0 0 0 / 8%);
  box-shadow: 0 4px 6px rgb(50 50 93 / 11%), 0 1px 3px rgb(0 0 0 / 8%);
}
.btn {
  display: inline-block;
  font-weight: 600;
  color: #525f7f;
  text-align: center;
  vertical-align: middle;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  background-color: transparent;
  border: 1px solid transparent;
  padding: 0.625rem 1.25rem;
  line-height: 1.5;
  border-radius: 0.375rem;
  -webkit-transition: color 0.15s ease-in-out, background-color 0.15s ease-in-out, border-color 0.15s ease-in-out,
    -webkit-box-shadow 0.15s ease-in-out;
  transition: color 0.15s ease-in-out, background-color 0.15s ease-in-out, border-color 0.15s ease-in-out,
    -webkit-box-shadow 0.15s ease-in-out;
  transition: color 0.15s ease-in-out, background-color 0.15s ease-in-out, border-color 0.15s ease-in-out,
    box-shadow 0.15s ease-in-out;
  transition: color 0.15s ease-in-out, background-color 0.15s ease-in-out, border-color 0.15s ease-in-out,
    box-shadow 0.15s ease-in-out, -webkit-box-shadow 0.15s ease-in-out;
}
a,
a:hover {
  text-decoration: none;
}
a {
  color: #5e72e4;
  background-color: transparent;
}
*,
:after,
:before {
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}
user agent stylesheet a:-webkit-any-link {
  color: -webkit-link;
  cursor: pointer;
  text-decoration: underline;
}
.text-center {
  text-align: center !important;
}
.card {
  position: absolute;
  bottom: 65px;
  /* left: 40px; */
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -ms-flex-direction: column;
  flex-direction: column;
  min-width: 0;
  word-wrap: break-word;
  background-color: #fff;
  background-clip: border-box;
  border: 1px solid rgba(0, 0, 0, 0.05);
  border-radius: 0.375rem;
}
body {
  margin: 0;
  font-family: Open Sans, sans-serif;
  font-size: 1rem;
  font-weight: 400;
  line-height: 1.5;
  color: #525f7f;
  text-align: left;
  /* background-color: #f8f9fe; */
}
</style>
<script>
export default {
  data() {
    return {};
  },
  methods: {},
};
</script>
}
