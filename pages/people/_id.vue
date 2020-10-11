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
        <div class="person__quotes">
          <b>Цитаты:</b>
          <p v-for="(item, i) in quotes" :key="item + i">- {{item.quote}}</p>
        </div>
      </div>
    </div>
    <div v-else>
      <spinner />
    </div>
  </div>
</template>

<script>
import Spinner from "@/components/Spinner/Spinner";
export default {
  components: {Spinner},
  data() {
    return {
      loading: true,
      person: [],
      quotes: []
    }
  },
  async mounted() {
    await this.$axios.get(`/characters/${this.$route.params.id}`)
      .then(res => this.person = res.data);
    await this.$axios.get(`/quote?author=${this.person[0].name}`)
      .then(res => this.quotes = res.data);
    this.loading = false;
  }
}
</script>

<style scoped lang="scss">
.person {
  width: 700px;
  padding: 20px;
  margin-top: 40px;
  background: white;
  &__quotes {
    b {
      width: 100%;
      display: block;
      margin-bottom: 20px;
      font-size: 30px;
      text-align: center;
    }
    p {
      margin-top: 5px;
    }
  }
  &__img {
    width: 100%;
    height: 500px;
    margin: 0 auto;
    background-size: cover;
    background-repeat: no-repeat;
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
