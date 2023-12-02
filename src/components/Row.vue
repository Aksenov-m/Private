<script setup>
import Cell from "./Cell.vue";
const props = defineProps(["data"]);

// Создаем новый объект, исключая указанные свойства
const { discount, order_sum, order_payed, pay_status, courier_comment, inner_comment, ...newObject } = props.data;

// Создаем новый объект с добавлением массива "pay" перед "courier_comment"
const newData = {
  ...newObject,
  pay: [ discount, order_sum, order_payed, pay_status ],
  courier_comment,
  inner_comment
};


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
      v-for="(value, key, index) in newData"
      :key="index"
      :content="value"
      :class="key"
    />
    <li v-if="remainingTime(props.data.dates[0].end_date) < 0" class="cell">
      <p class="text">
        Завершилось
        {{ Math.abs(remainingTime(props.data.dates[0].end_date)) }} дней назад
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
