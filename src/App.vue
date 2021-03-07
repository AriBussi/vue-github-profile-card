<template>
  <InputArea @userSubmition="updateUser" />
  <ProfileCard :githubUser="githubUser" />
</template>

<script>
import InputArea from "./components/InputArea";
import ProfileCard from "./components/ProfileCard.vue";

export default {
  name: "App",
  components: {
    InputArea,
    ProfileCard,
  },
  data() {
    return {
      githubUser: "AriBussi",
    };
  },
  methods: {
    updateUser(user) {
      this.githubUser = user;
    },
  },
};
</script>

<style>
body {
  height: 100vh;
  margin: 0;
  font-size: 16px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #535353;
  background-color: #eeeeee;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

h1 {
  font-size: 26px;
  margin-bottom: 2px;
  display: inline-block;
}

i {
  display: inline-block;
  font-size: 20px;
  cursor: pointer;
}
</style>
