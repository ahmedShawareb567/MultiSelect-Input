<template lang="pug">
.routeLoading(v-if="loading")
  .routeLoading-progress(:style="{'width': progressLength}")
  .routeLoading-circle
    .d-flex
      Loading
</template>
<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "RouteLoader",
  data() {
    return {
      loading: true,
      progressLength: 100,
    };
  },
  methods: {
    start() {
      this.loading = true;
    },
    finish() {
      setTimeout(() => {
        this.loading = false;
      }, 3000);
    },
    increase(value) {
      this.progressLength = value;
    },
  },
});
</script>
<style lang="scss">
.routeLoading {
  position: fixed;
  top: 0rem;
  right: 0rem;
  width: 100%;
  height: auto;
  z-index: 9999;
  &-progress {
    height: 0.2rem;
    background-color: red;
    transition: all 0.2s ease-in-out;
  }
  &-circle {
    padding: 0.5rem 1rem;
  }
}
</style>
