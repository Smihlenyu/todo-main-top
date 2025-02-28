<template>
  <div class="app"><HomePage /></div>
</template>

<script>
import HomePage from "./views/HomePage.vue";

export default {
  name: "App",
  components: {
    HomePage,
  },
};
</script>

<style>
@import "@/assets/style/main.scss";

.app {
}
</style>
