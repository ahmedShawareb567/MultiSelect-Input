<template lang="pug">
.checkInput
  input.checkInput-input.d-none(type="checkbox" ref="currentCheckBox" id="currentCheckBox")
  label.checkInput-label(for="currentCheckBox")
    .checkInput-icon: svgIcon(name="check-solid")

  label(for="currentCheckBox").checkInput-text {{label}}

</template>
<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "CheckInput",
  props: {
    label: {
      type: String,
      default: "اختر",
    },
  },
});
</script>
<style lang="scss">
.checkInput {
  display: flex;
  align-items: center;
  user-select: none;
  &-label {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 2rem;
    height: 2rem;
    border: 0.1rem solid #000;
    cursor: pointer;
    transition: all 0.1s ease-in-out;
  }
  &-icon {
    opacity: 0;
    .icon {
      width: 1.2rem !important;
      height: 1.2rem !important;
      fill: #fff !important;
    }
  }
  &-text {
    padding: 0rem 0.5rem;
    margin-bottom: 0rem;
  }
  &-input {
    &:checked ~ .checkInput-label {
      background-color: red;
      border-color: red;

      .checkInput {
        &-icon {
          opacity: 1;
        }
      }
    }
  }
}
</style>
