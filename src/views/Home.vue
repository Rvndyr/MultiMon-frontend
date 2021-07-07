<template>
  <div class="home">
    <!-- <section v-if="!twitchAccessToken"> -->
    <section>
      <main class="container text-center">
        <h1>Welcome!</h1>
        <h2>Please Sign in</h2>
        <a
          class="btn btn-lg btn-secondary"
          href="https://id.twitch.tv/oauth2/authorize?client_id=eliq1ssshmd7dc0z0ohal5zz8pszlc&redirect_uri=http://localhost:8080&response_type=code&scope=user:read:email%20user:read:follows"
        >
          Sign in with Twitch
        </a>
      </main>
    </section>
    <div class="row">
      <div class="col-sm p-3 border-end border-dark" v-if="twitchAccessToken">
        <span><h3>Followers:</h3></span>

        <div class="border" v-for="follow in follows" v-bind:key="follow.id">
          <div v-on:click="twitchPlayer(follow)">
            <!-- {{ follow.user_name }} -->
            <ol class="list-group">
              <li class="list-group-item-action d-flex justify-content-between align-items-start">
                <div class="ms-2 me-auto">
                  <div class="fw-bold">{{ follow.user_name }}</div>
                  Playing: {{ follow.game_name }} | Viewer Count: {{ follow.viewer_count }}
                </div>
              </li>
            </ol>
          </div>
        </div>
      </div>

      <div class="col-sm p-3 border-start border-dark">
        <!-- Show the videoPlayer from clicked Follower -->
        <span><h3>Twitch Player:</h3></span>
        <div v-for="follow in follows" v-bind:key="follow.id">
          <div v-bind:id="follow.user_id"></div>
        </div>
      </div>
      <!-- <div id="chat-`+ follow.user_name + `" class="stream_chat">
        <iframe
          frameborder="0"
          scrolling="no"
          id="chat-213670810-embed"
          src="https://twitch.tv/embed/puresobertv/chat?parent=localhost:8080"
          height="100%"
          width="100%"
        ></iframe>
      </div> -->

      <div id="120244187" class="col-sm border-dark">
        <button
          class="btn btn-primary"
          type="button"
          data-bs-toggle="offcanvas"
          data-bs-target="#offcanvasScrolling"
          aria-controls="offcanvasScrolling"
          v-on:click="twitchChat()"
        >
          Open Chat
        </button>
      </div>
    </div>
    <!-- Offcanvas Modal -->
    <div
      class="offcanvas offcanvas-end"
      data-bs-scroll="true"
      data-bs-backdrop="false"
      tabindex="0"
      id="offcanvasScrolling"
      aria-labelledby="offcanvasScrollingLabel"
    >
      <div class="offcanvas-header">
        <h5 class="offcanvas-title" id="offcanvasScrollingLabel">Twitch Chat</h5>
        <button type="button" class="btn-close text-reset" data-bs-dismiss="offcanvas" aria-label="Close"></button>
      </div>
      <div class="offcanvas-body">
        <!-- Nav inside offcanvas modal - This is where chat goes -->

        <ul class="nav nav-tabs" id="myTab" role="tablist">
          <li class="nav-item" role="presentation">
            <button
              class="nav-link active"
              id="home-tab"
              data-bs-toggle="tab"
              data-bs-target="#home"
              type="button"
              role="tab"
              aria-controls="home"
              aria-selected="true"
            >
              <div>Chat 1</div>
            </button>
          </li>
          <li class="nav-item" role="presentation">
            <button
              class="nav-link"
              id="profile-tab"
              data-bs-toggle="tab"
              data-bs-target="#profile"
              type="button"
              role="tab"
              aria-controls="profile"
              aria-selected="false"
            >
              <div>Chat 2</div>
            </button>
          </li>
        </ul>
        <div class="tab-content" id="myTabContent">
          <div class="tab-pane fade show active" id="home" role="tabpanel" aria-labelledby="home-tab">
            <iframe
              :id="`chat-${streams[0].user_id}-embed`"
              frameborder="0"
              scrolling="no"
              class="chatcanvas"
              :src="`https://www.twitch.tv/embed/${streams[0].user_name}/chat?parent=localhost`"
              allow-storage-access-by-user-activation="true"
              v-if="streams.length > 0"
            ></iframe>
          </div>
          <div class="tab-pane fade" id="profile" role="tabpanel" aria-labelledby="profile-tab">
            <iframe
              :id="`chat-${streams[1].user_id}-embed`"
              frameborder="0"
              scrolling="no"
              class="chatcanvas"
              :src="`https://www.twitch.tv/embed/${streams[1].user_name}/chat?parent=localhost`"
              allow-storage-access-by-user-activation="true"
              v-if="streams.length > 1"
            ></iframe>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
iframe {
  border: 0 none;
}

.chatcanvas {
  float: right;
  width: 350px;
  height: 85vh;
  margin: 0px;
  /* margin-left: -100px; */
  padding: 0;
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
          // console.log("Twitch user info", response.data);
          this.follows = response.data.follows;
          // console.log(this.follows[0].user_name);
        });
    }
  },
  mounted() {},
  methods: {
    twitchPlayer: function (follow) {
      // console.log("TwitchPlayer Function", follow);
      let options = {
        width: 950,
        height: 600,
        channel: follow.user_name,
        // only needed if your site is also embedded on embed.example.com and othersite.example.com
        parent: ["embed.example.com", "othersite.example.com"],
      };
      // change Embed to Player to remove chat from video
      let player = new Twitch.Player(follow.user_id, options);
      player.setVolume(0.5);
      // console.log("This is the clicked Player:", player);
      // console.log("This is the clicked iFrame:", player._iframe);
      follow.player = player;
      this.streams.push(follow);

      // Remove a stream if more than 2: delete iFrame from streams array
      if (this.streams.length === 3) {
        this.streams[0].player._iframe.remove();
        this.streams[0].shift();
      }
    },
    twitchChat: function () {},
  },
};
</script>
