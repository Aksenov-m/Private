<script setup>
const props = defineProps(["content", "class"]);
</script>

<template>
  <li class="cell" :class="props.class">
    <p class="text">{{ props.content }}</p>
  </li>
</template>

<style scoped>

.cell {
    background-color: rgba(255, 255, 255, 1);
}
.text {
  font-weight: 400;
  font-size: 10px;
  line-height: 16px;
  color: #000000;
}
.client_name p, 
.o_id p 
{
color: blue;
}
</style>