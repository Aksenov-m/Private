<script setup>
const props = defineProps(["content", "class"]);

function formatDate(inputDate) {
  // Преобразуем строку в объект Date
  let dateObj = new Date(inputDate);

  // Получаем месяц в числовом формате (от 0 до 11)
  let month = dateObj.getMonth();

  // Массив с названиями месяцев
  let monthNames = [
    "янв", "фев", "мар", "апр", "май", "июн", "июл", "авг", "сен", "окт", "ноя", "дек"
  ];

  // Форматируем дату
  let formattedDate = (month + 1) + "." + monthNames[month];

  return formattedDate;
}


</script>

<template>
  <ul class="cell__column" v-if="props.class === 'tariff'">
    <li v-for="(value, index) in props.content" :key="index">
      <p class="text">{{ value }}</p>
    </li>
  </ul>
  <ul class="cell__column_diets" v-else-if="props.class === 'diets'">
    <li v-for="(value, index) in props.content" :key="index">
      <p class="text">{{ value }}</p>
    </li>
  </ul>
  <!-- <ul
    class="cell__column_pay"
    v-else-if="props.class === 'order_payed'"
  >
    <li class="cell">
      <p class="text">{{ orderDetails.order_payed }}</p>
    </li>
    <li class="cell">
      <p class="text">{{ orderDetails.order_payed }}</p>
    </li>
    <li class="cell">
      <p class="text">{{ orderDetails.discount }}</p>
    </li>
  </ul> -->
  <ul class="cell" :class="props.class" v-else-if="props.class === 'dates'">
    <li v-for="(value, index) in props.content" :key="index">
      <p class="text">{{ formatDate(value.start_date) + ' - ' + formatDate(value.end_date) }}</p>
    </li>
  </ul>
  <li v-else class="cell" :class="props.class">
    <p class="text">{{ props.content }}</p>
  </li>
</template>

<style>
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
.o_id p {
  color: blue;
}

.cell__column_pay {
  display: flex;
  flex-direction: column;
}
</style>