<template>
  <div class="home-header">
    <NLink to="/" class="home-header__back" v-if="this.$route.path !== '/'">Домой</NLink>
    <h2 class="home-header__title">Breaking Bad</h2>
  </div>
</template>

<style scoped lang="scss">
.home-header {
  text-align: center;
  position: relative;
  &__title {
    font-size: 44px;
    font-weight: bold;
    color: #fff;
  }
  &__back {
    position: absolute;
    top: 20px;
    left: 6%;
    text-decoration: none;
    color: white;
    font-size: 18px;
  }
}
</style>
