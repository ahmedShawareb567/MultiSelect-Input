<template lang="pug">
.checkBoxInput
  input(type="checkbox" id="checkbox-new")
  .checkBoxInput-content
    label(for="checkbox-new").checkBoxInput test

</template>
<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  data() {
    return {
      currentValue: "",
    };
  },
});
</script>
<style lang="scss">
.checkBoxInput {
  position: relative;
  input[type="checkbox"] {
    display: none;
  }
}
</style>
