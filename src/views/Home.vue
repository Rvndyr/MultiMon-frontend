<template>
  <div class="home">
    <section>
      <b-avatar
        class="d-flex iconWeight"
        size="88px"
        :src="currentUser.profile_image_url"
        v-bind:key="currentUser.id"
      ></b-avatar>
      <span class="fw-bold iconWeight">{{ currentUser.display_name }}</span>
    </section>
    <div class="row">
      <div class="col-sm p-3" v-if="twitchAccessToken">
        <span class="ml-1"><h3>Followed Channels:</h3></span>
        <div v-for="follow in follows" v-bind:key="follow.id">
          <div @click="twitchPlayer(follow)">
            <ol class="list-group bg-transparent">
              <li class="list-group-item-action d-flex align-items-start">
                <div class="ms-2 me-auto followersWeight">
                  <div class="fw-bold followersSubWeight">
                    {{ follow.user_name }}
                    <div class="spinner-grow spinner-grow-sm text-danger" role="status">
                      <span class="visually-hidden">Loading...</span>
                    </div>
                  </div>
                  Playing: {{ follow.game_name }} | Viewers: {{ follow.viewer_count }}
                </div>
              </li>
            </ol>
          </div>
        </div>
      </div>
      <!-- Show the videoPlayer from clicked Follower -->
      <div class="col-sm p-3">
        <span><h3>Twitch Player:</h3></span>
        <div v-for="follow in follows" v-bind:key="follow.id">
          <div v-bind:id="follow.user_id"></div>
        </div>
        <div>
          <b-row class="d-flex align-items-center">
            <b-col class="ml-auto">
              <b-button v-if="sortedStreams.length >= 2" @click="swapPlayerDown(sortedStreams)" class="removeStylesBtn">
                <b-icon icon="arrow-down" animation="cylon-vertical" font-scale="3"></b-icon>
              </b-button>
              <b-button v-if="sortedStreams.length >= 2" class="removeStylesBtn">
                <b-icon icon="arrow-up" animation="cylon-vertical" font-scale="3"></b-icon>
              </b-button>
            </b-col>
          </b-row>
        </div>
      </div>

      <div class="col-sm">
        <b-button
          class="btn btn-secondary"
          type="button"
          data-bs-toggle="offcanvas"
          data-bs-target="#offcanvasScrolling"
          aria-controls="offcanvasScrolling"
        >
          <b-icon icon="chat-right-dots"></b-icon>
          Open Chat
        </b-button>
      </div>
    </div>
    <!-- Offcanvas Modal -->
    <div
      class="offcanvas offcanvas-end chatoffbody"
      data-bs-scroll="true"
      data-bs-backdrop="false"
      tabindex="0"
      id="offcanvasScrolling"
      aria-labelledby="offcanvasScrollingLabel"
    >
      <div class="offcanvas-header chatoffbody">
        <h5 class="offcanvas-title text-white" id="offcanvasScrollingLabel">Twitch Chat</h5>
        <button type="button" class="btn-close text-reset" data-bs-dismiss="offcanvas" aria-label="Close"></button>
      </div>
      <div class="offcanvas-body chatOffMain">
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
              <div v-if="this.sortedStreams.length > 0">{{ this.sortedStreams[0].user_name }}</div>
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
              <div v-if="this.sortedStreams.length > 1">{{ this.sortedStreams[1].user_name }}</div>
            </button>
          </li>
        </ul>
        <div class="tab-content" id="myTabContent">
          <div class="tab-pane fade show active twitch-chat" id="home" role="tabpanel" aria-labelledby="home-tab">
            <iframe
              :id="`chat-${this.sortedStreams[0].user_id}-embed`"
              frameborder="0"
              scrolling="no"
              class="chatcanvas"
              :src="`https://www.twitch.tv/embed/${this.sortedStreams[0].user_name}/chat?parent=localhost`"
              allow-storage-access-by-user-activation="true"
              v-if="this.sortedStreams.length > 0"
            ></iframe>
          </div>
          <div class="tab-pane fade" id="profile" role="tabpanel" aria-labelledby="profile-tab">
            <iframe
              :id="`chat-${this.sortedStreams[1].user_id}-embed`"
              frameborder="0"
              scrolling="no"
              class="chatcanvas"
              :src="`https://www.twitch.tv/embed/${this.sortedStreams[1].user_name}/chat?parent=localhost`"
              allow-storage-access-by-user-activation="true"
              v-if="this.sortedStreams.length > 1"
            ></iframe>
          </div>
        </div>
      </div>
    </div>
    <footer class="footer pt-10 pb-5 mt-auto">
      <hr class="my-5" />
      <div class="align-items-center">
        <div class="col-md-6 small text-white">Copyright &copy; Multi-Mon.com 2021</div>
        <div class="col-md-6 small text-white">Made with 💙 : ☕️</div>
        <div class="col-md-6 small text-white">
          <b-link href="https://github.com/Rvndyr" target="_blank">
            <b-icon icon="github" variant="light" font-scale="2"></b-icon>
          </b-link>
        </div>
      </div>
    </footer>
  </div>
</template>
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Encode+Sans+SC:wght@600&display=swap");
html,
body,
span,
p,
button,
h5 {
  color: whitesmoke;
  font-family: "Encode Sans SC", sans-serif;
}
.followersWeight {
  color: #ffc5bb;
}
.followersSubWeight {
  color: whitesmoke;
}
.list-group-item-action:hover {
  background: #ba53de !important;
}
.iconWeight {
  margin: 3em 3em 0 5em;
}
iframe {
  border: 0 none;
}
.chatoffbody {
  background-color: #3b3b44;
}
.chatOffMain {
  background-color: transparent;
}
.nav-link:focus,
.nav-link:hover {
  color: #ba53de;
}
.chatcanvas {
  float: right;
  width: 350px;
  height: 85vh;
  margin: 0px;
  padding: 0;
}
.removeStylesBtn {
  background: none;
  color: inherit;
  border: none;
  padding: 0;
  font: inherit;
  cursor: pointer;
  outline: inherit;
}
.removeStylesBtn:hover {
  background: none;
  color: #fff;
  border: none;
  padding: 0;
  font: inherit;
  cursor: pointer;
  outline: inherit;
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
      sortedStreams: [],
      currentUser: {},
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
          console.log("res data", response.data);
          this.currentUser = response.data.user;
          this.follows = response.data.follows;
          console.log("After Twitch_access_token runs", this.follows);
        });
    }
  },
  mounted() {},
  methods: {
    twitchPlayer: function (follow) {
      let options = {
        width: 950,
        height: 600,
        channel: follow.user_name,
        parent: [],
      };
      // change Embed to Player to remove chat from video
      let player = new Twitch.Player(follow.user_id, options);
      player.setVolume(0.5);
      follow.player = player;
      console.log(follow);
      this.streams.push(follow);

      this.sortedStreams = this.streams.sort((a, b) => b - a);

      for (let i = 0; i < this.sortedStreams.length; i++) {
        console.log("Logging sortedStreams:", this.sortedStreams[i].user_name);
        // Remove a stream if more than 2: delete iFrame from streams array
        // replace chat modal with new clicked person
        if (this.sortedStreams.length === 3) {
          this.sortedStreams[i].player._iframe.remove();
          this.sortedStreams.shift();
        }
      }
    },
    swapPlayerDown: function (sortedStreams) {
      console.log("SwappedStreams button", sortedStreams);
      let swappedStream = this.sortedStreams[0];

      this.sortedStreams[0] = this.sortedStreams[1];
      this.sortedStreams[1] = swappedStream;
      document.getElementById(`${this.sortedStreams[0].user_id}`).src = document.getElementById(
        `${this.sortedStreams[0].user_id}`
      ).src;

      console.log("Swapped Down!");
    },
  },
};
</script>
