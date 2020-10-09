<template>
  <div class="tabs">
    <ui-button v-for="(item, i) in tabs" :key="item + i" @click="$emit('click', item.active)">{{item.title}}</ui-button>
  </div>
</template>
<script>
import UiButton from "@/components/UI/UIButton";
export default {
  props: ['tabs'],
  components: {UiButton}
}
</script>

<style scoped lang="scss">
.tabs {
  text-align: center;
  margin-top: 20px;
}
</style>
