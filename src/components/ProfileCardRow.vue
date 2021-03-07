<template>
  <div class="profile_card--row">
    <ProfileCardIcon :icon="icon" :tooltip="tooltip" />
    <p>{{ info }}</p>
  </div>
</template>

<script>
import ProfileCardIcon from "./ProfileCardIcon";
export default {
  name: "profile_card_row",
  props: {
    icon: {
      required: true,
      type: String,
    },
    info: {
      type: String,
    },
    tooltip: {
      type: String,
    },
  },
  components: {
    ProfileCardIcon,
  },
};
</script>

<style>
.profile_card--row {
  display: flex;
  align-items: baseline;
  max-width: 80%;
  margin: 0 auto;
}
.profile_card--row p {
  display: inline-block;
  margin: 10px 0;
  text-align: left;
}

.profile_card--row i {
  width: 20px;
  height: 20px;
  margin-right: 12px;
}
</style>