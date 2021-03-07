<template>
  <div class="profile_card--icon">
    <i
      @mouseenter="toggleTooltip"
      @mouseout="toggleTooltip"
      :class="`fas fa-${icon}`"
    ></i>
    <span class="tooltip" v-if="tooltipOn">{{ tooltip }}</span>
  </div>
</template>

<script>
export default {
  name: "profile_card_icon",
  props: {
    icon: {
      required: true,
    },
    tooltip: {
      type: String,
    },
  },
  data() {
    return {
      tooltipOn: false,
    };
  },
  methods: {
    toggleTooltip() {
      this.tooltipOn = !this.tooltipOn;
    },
  },
};
</script>

<style>
.profile_card--icon {
  position: relative;
}

.profile_card--icon .tooltip {
  position: absolute;
  display: inline-block;
  background-color: rgb(193, 231, 233);
  padding: 5px 10px;
  border-radius: 12px;
  top: -35px;
  left: -10px;
}
</style>