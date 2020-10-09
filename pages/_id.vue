<template>
  <div class="container info">
    <div class="info__tabs">
      <button v-for="(item, i) in tabs" :key="item + i" @click="active = item.active">{{item.title}}</button>
    </div>
    <div class="info__block" v-if="!loading">
      <NLink class="info__item char" v-for="(item, i) in people" :to="`/people/${item.char_id}`" v-if="active === 'char'" :key="item + i" :style="`background-image: url(${item.img});`">
        <div>Имя: {{item.name}}</div>
        <p>Ник: {{item.nickname}}</p>
        <p>Статус: {{item.status}}</p>
        <div>Дата рождения: {{item.birthday}}</div>
      </NLink>
      <div class="info__item death" v-for="(item, i) in deaths" v-if="active === 'death'" :key="item + i">
        <div>Имя: {{item.death}}</div>
        <p>Причина: {{item.cause}}</p>
        <div>Ответственность: {{item.responsible}}</div>
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
      active: 'char',
      loading: true,
      tabs: [
        { title: 'Characters', active: 'char' },
        { title: 'Deaths', active: 'death' },
      ],
      data: [],
      people: [],
      episode: '',
      deaths: []
    }
  },
  async mounted() {
    await fetch(`https://breakingbadapi.com/api/episodes/${this.$route.params.id}`)
      .then(data => data.json())
      .then(res => {
        this.episode = res[0].episode;
        fetch(`https://breakingbadapi.com/api/characters?category=${res[0].series}`)
          .then(data => data.json())
          .then(res => this.people = res);
      })
    await fetch(`https://breakingbadapi.com/api/deaths`)
      .then(data => data.json())
      .then(res => this.deaths = res);
    this.loading = false;
  },
  computed: {
    FilterDeath() {
      return this.deaths.filter(item => item.episode == this.episode);
    }
  }
}
</script>

<style scoped lang="scss">
.info__tabs {
  text-align: center;
  margin-top: 20px;
  button {
    width: 150px;
    height: 50px;
    border: none;
    background: white;
    font-size: 18px;
    border-radius: 5px;
    cursor: pointer;
    margin-top: 20px;
    margin-left: 20px;
  }
}
.info__block {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin-top: 40px;
}
.char {
  &:hover {
    & > * {
      display: none;
    }
    &::after {
      background: rgba(0,0,0, .1);
    }
  }
}
.death {
  background: url("https://sun9-19.userapi.com/c304804/u165296456/a_38bf1304.jpg?ava=1") no-repeat;
  background-size: 100%;
}
.info__item {
  flex: 1 1 300px;
  height: 300px;
  margin: 10px;
  text-align: center;
  padding: 0 20px;
  background-repeat: no-repeat;
  background-size: cover;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  color: #fff;
  position: relative;
  cursor: pointer;
  > * {
    position: relative;
    z-index: 99;
    margin-top: 5px;
  }
  &::after {
    content: '';
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    background: rgba(0,0,0, .5);
  }
}
</style>
