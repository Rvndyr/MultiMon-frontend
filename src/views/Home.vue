<template>
  <div class="home">
    <section v-if="!twitchAccessToken">
      <!-- <div> -->
      <main class="container text-center">
        <h1>Welcome!</h1>
        <h2>Please Sign in</h2>
        <button
          class="btn btn-lg btn-secondary"
          href="https://id.twitch.tv/oauth2/authorize?client_id=eliq1ssshmd7dc0z0ohal5zz8pszlc&redirect_uri=http://localhost:8080&response_type=code&scope=user:read:email%20user:read:follows"
        >
          Sign in with Twitch
        </button>
      </main>
    </section>
    <div class="row">
      <div class="col-sm border-end border-dark" v-if="twitchAccessToken">
        <span><h3>Followers:</h3></span>

        <div class="border" v-for="follow in follows" v-bind:key="follow.id">
          <div v-on:click="twitchPlayer(follow)">
            <!-- {{ follow.user_name }} -->
            <ol class="list-group">
              <li class="list-group-item-action d-flex justify-content-between align-items-start">
                <div class="ms-2 me-auto">
                  <div class="fw-bold">{{ follow.user_name }}</div>
                  Playing: {{ follow.game_name }}
                </div>
              </li>
            </ol>
          </div>
        </div>
      </div>

      <div class="col-sm border-start border-dark">
        <!-- Show the videoPlayer from clicked Follower -->
        <span><h3>Twitch Player:</h3></span>
        <div v-for="follow in follows" v-bind:key="follow.id">
          <div v-bind:id="follow.user_id"></div>
        </div>
      </div>
      <!-- <div class="col-sm border border-dark">
        <iframe
          src="https://www.twitch.tv/embed/destroy/chat?parent=http://localhost:8080"
          allow-same-origin="true"
          height="500"
          width="350"
        ></iframe>
      </div> -->
    </div>
  </div>
</template>

<style>
.welcome-btn {
  color: #6610f2;
}
</style>

<script>
/* global Twitch */
import axios from "axios";
export default {
  data: function () {
    return {
      twitchAccessToken: null,
      follows: [],
      streams: [],
    };
  },
  created: function () {
    var twitchCode = this.$route.query.code;
    console.log("The twitch Code is ", twitchCode);
    if (twitchCode) {
      var params = { code: twitchCode };
      axios.post("http://localhost:3000/twitch_authorize", params).then((response) => {
        console.log("twitch access token", response.data);
        localStorage.setItem("twitch_access_token", response.data.access_token);
        this.$router.push("/");
      });
    }
    this.twitchAccessToken = localStorage.getItem("twitch_access_token");
    console.log("Helloppp", this.twitchAccessToken);
    if (this.twitchAccessToken) {
      // Get user info
      axios
        .get("http://localhost:3000/twitch_user_info?twitch_access_token=" + this.twitchAccessToken)
        .then((response) => {
          console.log("Twitch user info", response.data);
          this.follows = response.data.follows;
          // console.log(this.follows[0].user_name);
        });
    }
  },
  mounted() {},
  methods: {
    twitchPlayer: function (follow) {
      console.log("TwitchPlayer Function", follow);
      let options = {
        width: 950,
        height: 600,
        channel: follow.user_name,
        // only needed if your site is also embedded on embed.example.com and othersite.example.com
        parent: ["embed.example.com", "othersite.example.com"],
      };
      // change Embed to Player to remove chat from video
      let player = new Twitch.Embed(follow.user_id, options);
      player.setVolume(0.5);
      console.log("This is the clicked Player:", player);
      console.log("This is the clicked iFrame:", player._iframe);
      // Remove a stream if more than 2: delete iFrame from streams array
      this.streams.push(player);
      if (this.streams.length === 3) {
        this.streams[0]._iframe.remove();
        this.streams[0].shift();
      }
      console.log("These are the streams clicked:", this.streams);
    },
  },
};
</script>
