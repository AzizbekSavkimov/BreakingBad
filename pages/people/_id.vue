<template>
  <div class="container person">
    <div v-if="!loading">
      <div v-for="(item, i) in person" :key="item + i">
        <div class="person__img" :style="`background-image: url(${item.img})`"></div>
        <div class="person__title"><b>Имя:</b> {{item.name}}</div>
        <div><b>Ник:</b> {{item.nickname}}</div>
        <div><b>Категория:</b> {{item.category}}</div>
        <div><b>Дата рождения:</b> {{item.birthday}}</div>
        <div><b>Статус:</b> {{item.status}}</div>
        <div><b>Портрет:</b> {{item.portrayed}}</div>
      </div>
    </div>
    <div v-else>
      <spinner />
    </div>
  </div>
</template>

<script>
import Spinner from "@/components/Spienner/Spinner";
export default {
  components: {Spinner},
  data() {
    return {
      loading: true,
      person: [],
    }
  },
  async mounted() {
    await fetch(`https://breakingbadapi.com/api/characters/${this.$route.params.id}`)
      .then(data => data.json())
      .then(res => this.person = res);
    this.loading = false;
  }
}
</script>

<style scoped lang="scss">
.person {
  width: 400px;
  height: 500px;
  padding: 20px;
  margin-top: 40px;
  background: white;
  &__img {
    width: 100%;
    height: 200px;
    margin: 0 auto;
    background-size: 100%;
  }
  div {
    font-size: 18px;
    &:not(:first-child) {
      margin-top: 10px;
    }
  }
  &__title {
    margin-top: 30px !important;
  }
}
</style>
