<template>
  <div class="tabs">
    <ui-button v-for="(item, i) in tabs" :class="{'active': activeElem === item.active}" :key="item + i" @click="$emit('click', item.active)">{{item.title}}</ui-button>
  </div>
</template>
<script>
import UiButton from "@/components/UI/UIButton";
export default {
  props: ['tabs', 'activeElem'],
  components: {UiButton},
  mounted() {
    console.log(this.activeElem)
  }
}
</script>

<style scoped lang="scss">
.tabs {
  text-align: center;
  margin-top: 20px;
}
.active {
  background: green;
  opacity: .9;
  color: white;
}
</style>
