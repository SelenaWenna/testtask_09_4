<template lang="pug">
  td.cell(
    :class="options.status || options.defaultCellColor"
    @click="$emit('click')"
  )
</template>

<script>
export default {
  props: {
    options: Object
  }
}
</script>

<style scoped>
.cell {
  width: 50px;
  min-width: 50px;
  height: 50px;
  min-height: 50px;
  box-sizing: border-box;
  cursor: pointer;
  border: 1px solid lightgrey;
  padding: 0;
}
.active {
  background: mediumblue;
}
.available {
  background: limegreen;
}
.dark {
  background: black;
}
.light {
  background: white;
}
</style>

