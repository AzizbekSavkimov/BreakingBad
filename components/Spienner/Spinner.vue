<template>
  <div class="loading">Loading...</div>
</template>
<script>
export default {
  name: 'Spinner'
}
</script>
<style scoped lang="scss">
.loading {
  font-size: 20px;
  color: white;
  margin-top: 40px;
  text-align: center;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
</style>
