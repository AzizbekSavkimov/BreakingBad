<template>
  <div class="home">
    <home-header />
    <nuxt/>
  </div>
</template>
<script>
import HomeHeader from "@/components/Home/HomeHeader";
export default {
  components: {HomeHeader}
}
</script>
<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  outline: none;
}
body {
  background: #27ae60;
}
html {
  font-family: 'Open Sans';
}
.home {
  padding: 40px 0;
}
.container {
  max-width: 90%;
  margin: 0 auto;
}
</style>
