<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__user-name">@{{ user.username }}</h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>
      <div class="user-profile__follower-count">
        <strong>Followers: </strong>{{ followers }}
      </div>
      <button @click="followUser">Follow</button>
      <button @click="unFollowUser">Unfollow</button>
    </div>
    <div class="user-profile__user-twoot-wrapper">
      <TwootItem
        v-for="twoot in user.twoots"
        :key="twoot.id"
        :username="user.username"
        :twoot="twoot"
        @favorite="toggleFavorite"
      />
    </div>
  </div>
</template>

<script>
import TwootItem from "./TwootItem";
export default {
  name: "UserProfile",
  components: { TwootItem },
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "artiele",
        firstname: "Jester",
        lastname: "Artienda",
        email: "artiele@oocl.com",
        isAdmin: false,
        twoots: [
          { id: 1, content: "Twotter is amazing!" },
          { id: 2, content: "Subscribe now..." },
        ],
      },
    };
  },
  computed: {
    fullname() {
      return `${this.user.firstname} ${this.user.lastname}`;
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
    unFollowUser() {
      this.followers--;
    },
    toggleFavorite(id) {
      console.log(`Favorited tweet: ${id}`);
    },
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a new follower!`);
      }
    },
  },
  mounted() {
    this.followUser();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  padding: 50px 5%;
}
.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: wheat;
  border-radius: 5px;
  border: 1px solid #dfd4e8;
}
h1 {
  margin: 0;
}
.user-profile__admin-badge {
  background: purple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 px;
  font-weight: bold;
}
</style>
