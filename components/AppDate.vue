<template lang="pug">
.appDate
  .appDate-toggle(@click="openDatePicker()")
  .d-flex
    span
      svg(xmlns='http://www.w3.org/2000/svg' enable-background='new 0 0 24 24' height='24px' viewbox='0 0 24 24' width='24px' fill='#000000')
        g
          rect(fill='none' height='24' width='24')
        g
          path(d='M19,4h-1V2h-2v2H8V2H6v2H5C3.89,4,3.01,4.9,3.01,6L3,20c0,1.1,0.89,2,2,2h14c1.1,0,2-0.9,2-2V6C21,4.9,20.1,4,19,4z M19,20 H5V10h14V20z M9,14H7v-2h2V14z M13,14h-2v-2h2V14z M17,14h-2v-2h2V14z M9,18H7v-2h2V18z M13,18h-2v-2h2V18z M17,18h-2v-2h2V18z')
    .mx-2
      client-only
        Datepicker(v-model="dateTime" :language="en" ref="datePicker")

</template>
<script lang="ts">
import Vue from "vue";
import { en, ar } from "vuejs-datepicker/dist/locale";

export default Vue.extend({
  name: "AppDate",
  components: { Datepicker: () => import("vuejs-datepicker") },
  data() {
    return {
      dateTime: Date.now(),
      ar: ar,
      en: en,
    };
  },
  methods: {
    openDatePicker() {
      this.$refs.datePicker.showCalendar();
    },
  },
});
</script>

<style lang="scss">
$primary: red;
$white: #fff;
$cell-border-hover: red;

.appDate {
  position: relative;
  padding: 0.5rem 0rem;
  &-toggle {
    position: absolute;
    top: 0rem;
    right: 0rem;
    width: 100%;
    height: 100%;
    z-index: 9;
  }
  .vdp-datepicker {
    &.rtl {
      text-align: right !important;
    }
    input[type="text"] {
      border: none !important;
      outline: none !important;
      font-size: 0.8rem !important;
      font-weight: 500;
    }
    &__calendar {
      .month {
        font-size: 0.8rem !important;
        font-weight: 500;
      }
      .cell {
        &.day,
        &.month {
          &:hover {
            border-color: $cell-border-hover !important;
          }
        }
        &.selected {
          background-color: $primary !important;
          color: $white !important;
        }
      }
    }
  }
}
</style>
