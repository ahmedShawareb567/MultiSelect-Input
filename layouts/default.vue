<template lang="pug">
div
    nuxt
</template>
<script>
export default {
  head() {
    const i18nSeo = this.$nuxtI18nSeo();
    return {
      htmlAttrs: {
        dir: "rtl",
        ...i18nSeo.htmlAttrs,
      },
      meta: [...i18nSeo.meta],
      link: [...i18nSeo.link],
    };
  },
};
</script>
<style lang="scss"></style>
