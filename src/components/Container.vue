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

const updatedData = data.map(item => {
  const { discount, order_sum, order_payed, pay_status, courier_comment, inner_comment, dates, ...newItem } = item;
  const remaining_days = dates.map(date => remainingTime(date.end_date));
  return {
    ...newItem,
    dates,
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

const sortedData = updatedData.sort((a, b) => {
  const remainingDaysA = a.remaining_days[0];
  const remainingDaysB = b.remaining_days[0];

  return remainingDaysA - remainingDaysB;
});

console.log("Original Data:", data);
console.log("Updated Data:", updatedData);
console.log("Sorted Data:", sortedData);

</script>

<template>
  <div>
    <Row v-for="(value, index) in sortedData" :key="index" :data="value">
    </Row>
  </div>
</template>

<style scoped></style>