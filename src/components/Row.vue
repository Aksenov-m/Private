<script setup>
import Cell from "./Cell.vue";
const props = defineProps(["data"]);

</script>

<template>
  <ul class="row">
    <Cell
      v-for="(value, key, index) in props.data"
      :key="index"
      :content="value"
      :class="key"
    />
  </ul>
</template>

<style scoped>
.row {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-around;
  list-style: none;
}
</style>
