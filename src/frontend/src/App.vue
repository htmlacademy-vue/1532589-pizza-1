<template>
  <div id="app">
    <index-views />
  </div>
</template>

<script>
import IndexViews from "@/views/Index.vue";
export default {
  name: "App",
  components: {
    IndexViews,
  },
};
</script>

<style lang="scss">
@import "~@/assets/scss/app";
</style>
