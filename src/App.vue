<template>
  <fodmap></fodmap>
</template>

<script>
import Fodmap from "./components/fodmap";

export default {
  name: "app",
  components: {
    Fodmap
  }
};
</script>

<style lang="scss">
body {
  font-family: "Source Sans Pro", "Helvetica Neue", Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0;
  color: #2c3e50;
  line-height: 1.8;
  font-size: 100%;
  background: #f6f6f6;
}

main {
  max-width: 500px;
  margin: 0 auto;
}

ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
</style>
