<template>
  <button class="ui-button" @click="$emit('click')"><slot /></button>
</template>
<script>
export default {
  name: 'uiButton'
}
</script>
<style scoped lang="scss">
.ui-button {
  width: 150px;
  height: 50px;
  border: none;
  background: white;
  font-size: 18px;
  border-radius: 5px;
  cursor: pointer;
  margin-top: 20px;
  margin-left: 20px;
  transition: .2s ease;
  &:hover {
    background: green;
    opacity: .6;
  }
}
</style>
