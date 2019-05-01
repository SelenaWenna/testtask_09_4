<template lang="pug">
  th.cell-header {{ headerY }}
</template>

<script>
export default {
  props: {
    headerY: String,
  }
}
</script>

<style scoped>
.cell-header {
  width: 35px;
  min-width: 35px;
  height: 50px;
  min-height: 50px;
  box-sizing: border-box;
  font-size: 20px;
  line-height: 1;
  font-weight: 400;
  padding-top: 15px;
  padding-bottom: 15px;
}
</style>

