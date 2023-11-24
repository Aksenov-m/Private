<script setup>
import Cell from "./Cell.vue";
const props = defineProps(["data"]);
</script>

<template>
    <ul><Cell v-for="(value, key, index) in props.data" :key="index" :content="value" :class="key"/></ul>
</template>

<style scoped></style>
