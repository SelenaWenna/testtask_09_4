<template lang="pug">
  tr
    th
    th.cell-header(v-for="x in headerX") {{ x }}
    th
</template>

<script>
export default {
  props: {
    headerX: {
      type: String,
      default: String('ABCDEFGH')
    }
  }
}
</script>

<style scoped>
.cell-header {
  width: 50px;
  min-width: 50px;
  height: 35px;
  min-height: 35px;
  box-sizing: border-box;
  font-size: 20px;
  font-weight: 400;
  padding-top: 7px;
  padding-bottom: 7px;
}
</style>

