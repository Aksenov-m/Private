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
  display: grid;
  grid-template-columns: 40px repeat(auto-fit, minmax(50px, 1fr));
  justify-content: stretch;
  align-items: center;
  width: 100%;
  list-style: none;
  border: 2px solid rgba(222, 226, 230, 1);
  margin: 0;
  padding: 0;
}

.row:nth-child(2n) {
  background-color: rgba(242, 242, 242, 1);
}
</style>
