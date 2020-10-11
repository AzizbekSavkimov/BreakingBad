<template>
  <section class="home-content container">
      <div v-if="!loading">
        <div class="home-search">
          <input type="text" class="home-search__input" v-model="input" placeholder="Введите название...">
          <button type="button" class="home-search__button">Искать</button>
        </div>
        <tabs :tabs="tabs" @click="active = $event" />
        <div class="content">
          <NLink v-for="(item, i) in FilterContent" class="content__item" v-if="item.season === active" :to="`/episodes/${item.episode_id}`" :key="item + i">
            <h3 class="content__item-title">{{item.title}}</h3>
            <div class="content__item-date">Дата выхода: <b>{{item.air_date}}</b></div>
            <div class="content__item-series">Серия: <b>{{item.series}}</b></div>
            <div class="content__item-episode">Эпизод: <b>{{item.episode}}</b></div>
          </NLink>
        </div>
      </div>
      <div v-else>
        <spinner />
      </div>
  </section>
</template>
<script>
import Spinner from "@/components/Spinner/Spinner";
import UiButton from "@/components/UI/UIButton";
import Tabs from "@/components/Shared/Tabs";

export default {
  name: 'homeContent',
  components: {Tabs, UiButton, Spinner},
  data() {
    return {
      input: '',
      active: '1',
      loading: true,
      tabs: [
        { title: 'Сезон 1', active: '1', btn: true, },
        { title: 'Сезон 2', active: '2', btn: false, },
        { title: 'Сезон 3', active: '3', btn: false, },
        { title: 'Сезон 4', active: '4', btn: false, },
        { title: 'Сезон 5', active: '5', btn: false, },
      ],
      content: [],
    }
  },
  mounted() {
    this.$axios.get('/episodes')
      .then(res => this.content = res.data);
    this.loading = false;
  },
  computed: {
    FilterContent() {
      if (this.input !== '') {
        return this.content.filter((item) => item.title.includes(this.input));
      } else {
        return this.content;
      }
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
.home-content {
  &__tabs {
    text-align: center;
    margin-top: 20px;
  }
  .content {
    display: flex;
    flex-wrap: wrap;
    margin-top: 40px;
    &__item {
      flex: 1 1 250px;
      min-height: 350px;
      margin: 10px;
      border-radius: 10px;
      background: white;
      font-size: 18px;
      padding: 20px;
      cursor: pointer;
      color: black;
      text-align: center;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      text-decoration: none;
      &:hover {
        text-decoration: underline;
      }
      > div {
        margin-top: 12px;
      }
      &-title {
        text-align: center;
        margin-bottom: 20px;
        height: 28px;
        overflow: hidden;
      }
      &-list {
        display: flex;
        li {
          list-style: none;
        }
      }
    }
  }
}
</style>
