<template lang="pug">
div
  .container.pt-xxl
    .row.justify-content-center
      .col-md-6
        div(style="padding-top:4rem;")
          MultiSelect(v-model="section" :options="options" @searchChange="searchChange" label="🎃 Add Category:")
</template>
<script>
export default {
  data() {
    return {
      section: [],
      options: [
        {
          value: 1,
          text: "Food"
        },
        {
          value: 2,
          text: "Animal"
        },
        {
          value: 3,
          text: "Weapons"
        }
      ]
    };
  },
  computed: {
    availableLocales() {
      return this.$i18n.locales.filter(i => i.code !== this.$i18n.locale);
    }
  },
  methods: {
    searchChange(value) {
      console.log(value);
    }
  }
};
</script>
<style lang="scss"></style>
