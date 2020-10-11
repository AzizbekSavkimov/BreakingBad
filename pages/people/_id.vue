<template>
  <div class="container person">
    <div v-if="!loading">
      <div v-for="(item, i) in person" :key="item + i">
        <div class="person__img" :style="`background-image: url(${item.img})`"></div>
        <div class="person__title"><b>Имя:</b> {{item.name}}</div>
        <div><b>Ник:</b> {{item.nickname}}</div>
        <div><b>Категория:</b> {{item.category}}</div>
        <div><b>Портрет:</b> {{item.portrayed}}</div>
        <div class="person__quotes">
          <h1>Цитаты:</h1>
          <p v-for="(item, i) in quotes" :key="item + i">- {{item.quote}}</p>
        </div>
        <div>
          <h1>Таймлайн</h1>
          <div class="timeline">
            <div class="timeline__item">
              <span class="timeline__item-title">Дата</span>
              <span class="timeline__item-circle"></span>
              <span class="timeline__item-info">{{item.birthday}}</span>
            </div>
            <div class="timeline__item">
              <span class="timeline__item-title">Эпизоды</span>
              <span class="timeline__item-circle"></span>
              <p class="timeline__item-info" v-for="(item, i) in episodes" :key="item + i">
                {{item.title}}
              </p>
            </div>
            <div class="timeline__item">
              <span class="timeline__item-title">Смерти</span>
              <span class="timeline__item-circle"></span>
              <p class="timeline__item-info" v-for="(item, i) in deaths" :key="item + i">{{item.death}}</p>
            </div>
            <div class="timeline__item">
              <span class="timeline__item-title">Статус</span>
              <span class="timeline__item-circle"></span>
              <span class="timeline__item-info">{{item.status}}</span>
            </div>
          </div>
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
      quotes: [],
      episodes: [],
      deaths: []
    }
  },
  async mounted() {
    await this.$axios.get(`/characters/${this.$route.params.id}`)
      .then(res => this.person = res.data);
    await this.$axios.get(`/quote?author=${this.person[0].name}`)
      .then(res => this.quotes = res.data);
    for (let i = 0; i < this.person[0].category.split(',').length; i++) {
      await this.$axios.get(`/episodes?series=${this.person[0].category.split(', ')[i]}`)
        .then(res => this.episodes = [...res.data]);
    }
    this.loading = false;
  },
}
</script>

<style scoped lang="scss">
.timeline {
  width: 100%;
  display: flex;
  margin-top: 40px !important;
  margin-bottom: 40px !important;
  position: relative;
  &::after {
    content: '';
    width: 100%;
    height: 6px;
    background: blue;
    border-radius: 5px;
    position: absolute;
    top: 0;
    left: 0;
  }
  &__item {
    position: relative;
    top: -27px;
    width: 25%;
    text-align: center;
    display: flex;
    flex-direction: column;
    margin-top: 0 !important;
    &-title {
      margin-bottom: 25px;
      font-size: 14px;
    }
    &-info {
      font-size: 15px;
    }
    &-circle {
      width: 4px;
      height: 20px;
      background: blue;
      position: absolute;
      top: 22px;
      left: 50%;
    }
  }
}
.person {
  width: 700px;
  padding: 20px;
  margin-top: 40px;
  background: white;
  h1 {
    text-align: center;
  }
  &__quotes {
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
  > div {
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
