<script setup>
import data from "../data/data.json";
import Row from "./Row.vue";

const remainingTime = (end_date) => {
  let endDate = new Date(end_date);
  let currentDate = new Date();
  let timeDifference = endDate - currentDate;
  let daysDifference = Math.floor(timeDifference / (1000 * 60 * 60 * 24));
  return daysDifference;
};

const updatedData = data.map((item) => {
  const {
    discount,
    order_sum,
    order_payed,
    pay_status,
    courier_comment,
    inner_comment,
    dates,
    ...newItem
  } = item;
  const remaining_days = dates.map((date) => remainingTime(date.end_date));
  return {
    ...newItem,
    dates,
    pay: [
      {
        discount,
        order_sum,
        order_payed,
        pay_status,
      },
    ],
    courier_comment,
    inner_comment,
    remaining_days,
  };
});

const sortedData = updatedData.sort((a, b) => {
  const remainingDaysA = a.remaining_days[0];
  const remainingDaysB = b.remaining_days[0];

  return remainingDaysA - remainingDaysB;
});

console.log("Original Data:", data);
console.log("Updated Data:", updatedData);
console.log("Sorted Data:", sortedData);

const nameCell = [
  "Номер",
  "Имя",
  "Диета",
  "Тариф",
  "Адрес",
  "Телефон",
  "Дата заказа",
  "Оплата",
  "Доставка",
  "Комментарий",
  "Статус заказа",
];
</script>

<template>
  <div>
    <div class="container__heading">
      <h1 class="heading" v-for="(value, index) in nameCell" :key="index">{{value}}</h1>
    </div>
    <Row v-for="(value, key, index) in sortedData" :key="index" :data="value">
    </Row>
  </div>
</template>

<style scoped>

.container__heading{
  display: grid;
  grid-template-columns: 40px repeat(auto-fit, minmax(50px, 1fr));
  align-items: center;
}
.heading{
  margin: 0 auto;
  width: 100%;
  height: 40px;
  background-color: cadetblue;
  font-weight: 500;
  font-size: 12px;
  line-height: 14px;
  text-align: center;
  border: 2px solid rgb(20, 20, 20);
  cursor: pointer;
}


</style>