<script setup>
import data from "../data/data.json";
import Row from "./Row.vue";
// const newData = JSON.parse(data);
// console.log(newData)
</script>

<template>
  <div>
    <Row v-for="(value, index) in data" :key="index" :data="value">
    </Row>
  </div>
</template>

<style scoped></style>
