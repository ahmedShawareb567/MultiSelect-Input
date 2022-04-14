<template lang="pug">
div
  .container.pt-xxl
    .row.justify-content-center
      .col-12.pt-4
        nuxt-link(to="/about") About
        nuxt-link(to="/") Home
      .col-md-6
        div(style="padding-top:4rem;")
          MultiSelect(v-model="section" :options="options" @searchChange="searchChange" label="🎃 Add Category:")

        select.form-select.mt-4
          option(value="null") choose
          option(value="2")  2
          option(value="3")  3

        .py-3
          AppDate

        .py-3
          ImagesUploader

        .d-flex.justify-content-center.align-items-center.py-3
          Loading
          Loading(type="wave")

        RouteLoader

        .custom-control.custom-checkbox.py-3
          input.custom-control-input(type="checkbox")

  .py-3
    RouteLoader
  .d-flex.justify-content-center.py-3
    CheckInput
</template>
<script>
export default {
  data() {
    return {
      section: [],
      options: [
        {
          value: 1,
          text: "Food",
        },
        {
          value: 2,
          text: "Animal",
        },
        {
          value: 3,
          text: "Weapons",
        },
      ],
      image: "",
    };
  },
  computed: {
    availableLocales() {
      return this.$i18n.locales.filter((i) => i.code !== this.$i18n.locale);
    },
  },
  methods: {
    searchChange(value) {
      console.log(value);
    },
  },
};
</script>
<style lang="scss">
.form-select {
  background-image: url("/arrow.svg") !important;
}
</style>
