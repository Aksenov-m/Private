<script setup>
import Cell from "./Cell.vue";
const props = defineProps(["data"]);

const remainingTime = (date) => {
  // Преобразуем строку начальной даты в объект Date
  let startDate = new Date(date);
  // Получаем текущую дату
  let currentDate = new Date();
  // Разница в миллисекундах
  let timeDifference = currentDate - startDate;
  // Преобразуем разницу в дни
  let daysDifference = Math.floor(timeDifference / (1000 * 60 * 60 * 24));
  return daysDifference;
};

// const orderDetails = {
//   discount: props.data.discount,
//   pay_status: props.data.pay_status,
//   order_payed:  props.data.order_payed,
// };
// console.log(props.data.discount)
</script>

<template>
  <ul class="row">
    <Cell
      v-for="(value, key, index) in props.data"
      :key="index"
      :content="value"
      :class="key"
    />
    <ul
    class="cell__column_pay"
  >
    <li class="cell">
      <p class="text">{{ props.data.discount }}</p>
    </li>
    <li class="cell">
      <p class="text">{{ props.data.pay_status }}</p>
    </li>
    <li class="cell">
      <p class="text">{{ props.data.order_payed }}</p>
    </li>
  </ul>
    <li v-if="remainingTime(props.data.dates[0].end_date) < 0" class="cell">
      <p class="text">
        Завершилось {{ Math.abs(remainingTime(props.data.dates[0].end_date)) }} дней назад
      </p>
    </li>
    <li v-else class="cell">
      <p class="text">
        заканчивается через
        {{ remainingTime(props.data.dates[0].end_date) }} дней
      </p>
    </li>
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
