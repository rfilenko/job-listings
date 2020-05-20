<template>
  <div class="app">
    <AppHeader />
    <nuxt />
    <AppFooter />
  </div>
</template>

<script>
import AppHeader from "~/components/AppHeader.vue";
import AppFooter from "~/components/AppFooter.vue";

export default {
  components: {
    AppHeader,
    AppFooter
  }
};
</script>
<style>
html {
  font-family: "Spartan", sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}

body {
  background: hsl(180, 52%, 96%);
  font-size: 15px;
  color: hsl(180, 14%, 20%);
}
.app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}
.container {
  margin: 0 auto;
  text-align: center;
  margin-top: 2rem;
}
</style>
