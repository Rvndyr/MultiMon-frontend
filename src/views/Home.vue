<template>
  <div class="home">
    <div v-if="!twitchAccessToken">
      <h1>Authorize Twitch</h1>
      <a
        href="https://id.twitch.tv/oauth2/authorize?client_id=eliq1ssshmd7dc0z0ohal5zz8pszlc&redirect_uri=http://localhost:8080&response_type=code&scope=user:read:email%20user:read:follows"
      >
        Authorize Twitch
      </a>
    </div>
    <div class="row">
      <div class="col-sm border border-dark" v-if="twitchAccessToken">
        Followers:
        <div v-for="follow in follows" v-bind:key="follow.id">
          <!-- {{ follow.user_name }} -->
          <div id="VideoSection">
            <div v-on:click="twitchPlayer(follow)" v-bind:id="follow.user_id">{{ follow.user_name }}</div>
          </div>
        </div>
      </div>

      <div class="col-sm border border-dark"><div id="31688366"></div></div>
      <div class="col-sm border border-dark">
        <iframe
          src="https://www.twitch.tv/embed/symfuhny/chat?parent=http://localhost:8080"
          allow-same-origin
          height="500"
          width="350"
        ></iframe>
      </div>
    </div>
  </div>
</template>

<style></style>

<script>
/* global Twitch */
import axios from "axios";
export default {
  data: function () {
    return {
      twitchAccessToken: [],
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
  mounted() {
    // Add script tag to head in HTML
    let twitchEmbed = document.createElement("script");
    twitchEmbed.setAttribute("src", "https://embed.twitch.tv/embed/v1.js");
    document.head.appendChild(twitchEmbed);
  },
  methods: {
    twitchPlayer: function (follow) {
      this.follow = follow;
      console.log("TwitchPlayer Function", this.follow);
      let options = {
        width: 854,
        height: 480,
        channel: follow.user_name,
        // only needed if your site is also embedded on embed.example.com and othersite.example.com
        parent: ["embed.example.com", "othersite.example.com"],
      };
      let player = new Twitch.Player(follow.user_id, options);
      player.setVolume(0.5);
      console.log(player);
    },
  },
};
</script>
