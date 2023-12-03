<script setup>
import data from "../data/data.json";
import Row from "./Row.vue";
// const data = JSON.parse(data);


const remainingTime = (end_date) => {
  // Преобразуем строку конечной даты в объект Date
  let endDate = new Date(end_date);
  // Получаем текущую дату
  let currentDate = new Date();
  // Разница в миллисекундах
  let timeDifference = endDate - currentDate;
  // Преобразуем разницу в дни
  let daysDifference = Math.floor(timeDifference / (1000 * 60 * 60 * 24));
  return daysDifference;
};



// Обновляем каждый объект в массиве
const updatedData = data.map(item => {
  const { discount, order_sum, order_payed, pay_status, courier_comment,
    inner_comment, dates, ...newItem } = item;
  const remaining_days = dates.map(date => remainingTime(date.end_date));
  return {
    ...newItem,
    pay: [
      {
        discount,
        order_sum,
        order_payed,
        pay_status
      }
    ],
    courier_comment,
    inner_comment,
    remaining_days
  };
});
console.log(updatedData)

</script>

<template>
  <div>
    <Row v-for="(value, index) in updatedData" :key="index" :data="value">
    </Row>
  </div>
</template>

<style scoped></style>
