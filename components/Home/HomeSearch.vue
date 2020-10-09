<template>
  <div class="home-search">
    <input type="text" class="home-search__input" v-model="value" placeholder="Введите название...">
    <button type="button" class="home-search__button">Искать</button>
  </div>
</template>
<script>
export default {
  name: 'homeSearch',
  data() {
    return {
      value: ''
    }
  },
}
</script>

<style scoped lang="scss">
.home-search {
  text-align: center;
  margin-top: 40px;
  &__input {
    width: 600px;
    height: 40px;
    border: none;
    border-radius: 5px;
    font-size: 16px;
    padding-left: 15px;
  }
  &__button {
    width: 100px;
    height: 40px;
    border: none;
    background: white;
    font-size: 16px;
    border-radius: 5px;
    cursor: pointer;
  }
}
</style>
