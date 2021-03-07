<template>
  <div id="profile_card--body">
    <img :src="user.avatar_url" />
    <div id="profile_card--title">
      <h1>{{ userName }}</h1>
      <ProfileCardIcon
        icon="calendar-day"
        :tooltip="`User since ${userSince}`"
      />
    </div>
    <div>
      <ProfileCardRow
        icon="street-view"
        :info="this.user.login"
        tooltip="Username"
      />
      <ProfileCardRow
        icon="map-marker-alt"
        :info="userLocation"
        tooltip="Location"
      />
      <ProfileCardRow icon="biohazard" :info="userBio" tooltip="Bio" />
    </div>
  </div>
</template>

<script>
import ProfileCardRow from "./ProfileCardRow";
import ProfileCardIcon from "./ProfileCardIcon";

export default {
  name: "profile_card",
  props: {
    githubUser: {
      type: String,
      required: true,
    },
  },
  components: {
    ProfileCardRow,
    ProfileCardIcon,
  },
  data() {
    return {
      user: "",
    };
  },
  watch: {
    githubUser() {
      this.getUserData();
    },
  },
  computed: {
    userName() {
      if (this.user) {
        return this.user.name || this.user.login;
      }
      return "";
    },
    userSince() {
      if (this.user) {
        return this.user.created_at.split("T")[0];
      }
      return "";
    },
    userLocation() {
      if (this.user) {
        return this.user.location || "Earth";
      }
      return "";
    },
    userBio() {
      if (this.user) {
        return this.user.bio || "No bio provided...";
      }
      return "";
    },
  },
  methods: {
    async getUserData() {
      const response = await fetch(
        `https://api.github.com/users/${this.githubUser}`
      );

      if (response.status === 404) {
        this.user = {
          created_at: "-T-",
          location: "-",
          name: "Not Found",
          login: "User Not Found",
          bio: "-",
          avatar_url: require("../assets/mrx.jpg"),
        };
        console.log(this.user);
      } else {
        this.user = await response.json();
        console.log(this.user);
      }
    },
  },
  created() {
    this.getUserData();
  },
};
</script>

<style>
#profile_card--body {
  box-shadow: 2px 2px 10px lightgray;
  border-radius: 12px;
  width: 300px;
  min-height: 440px;
  margin: 0 auto;
  background-color: #fafafa;
}

#profile_card--body img {
  max-width: 180px;
  border-radius: 50%;
  margin-top: 25px;
}

#profile_card--title {
  border-bottom: 2px solid #ababab;
  width: 75%;
  margin: 0 auto 12px auto;
  padding: 0 10px 5px 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

#profile_card--title i {
  margin-bottom: 2px;
  position: relative;
  top: 12px;
}
</style>
