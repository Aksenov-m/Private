<script setup>
const props = defineProps(["content", "class"]);

function formatDate(inputDate) {
  // Преобразуем строку в объект Date
  let dateObj = new Date(inputDate);

  // Получаем месяц в числовом формате (от 0 до 11)
  let month = dateObj.getMonth();

  // Массив с названиями месяцев
  let monthNames = [
    "янв",
    "фев",
    "мар",
    "апр",
    "май",
    "июн",
    "июл",
    "авг",
    "сен",
    "окт",
    "ноя",
    "дек",
  ];

  // Форматируем дату
  let formattedDate = month + 1 + "." + monthNames[month];

  return formattedDate;
}

</script>

<template>
  <ul class="cell__column" :class="props.class" v-if="props.class === 'tariff'">
    <li v-for="(value, index) in props.content" :key="index" class="column">
      <p class="text">{{ value }}</p>
    </li>
  </ul>

  <ul
    class="cell__column"
    :class="props.class"
    v-else-if="props.class === 'diets'"
  >
    <li v-for="(value, index) in props.content" :key="index" class="column">
      <p class="text">{{ value }}</p>
      <hr v-show="props.content.length > 1 && index != props.content.length - 1"/>
    </li>
  </ul>

  <ul
    class="cell__column"
    :class="props.class"
    v-else-if="props.class === 'dates'"
  >
    <li v-for="(value, index) in props.content" :key="index" class="column">
      <p class="text">
        {{ formatDate(value.start_date) + " - " + formatDate(value.end_date) }}
      </p>
    </li>
  </ul>
  <ul
    class="cell__column"
    :class="props.class"
    v-else-if="props.class === 'pay'"
  >
    <li
      v-for="(value, key, index) in props.content[0]"
      :key="index"
      class="column"
    >
      <p class="text" v-if="index === 0">Скидка {{ value }}%</p>
      <p class="text" v-else-if="index === 1">Стоим.: {{ value }}р</p>
      <p class="text" v-else-if="index === 2">Долг: {{ value }}р</p>
    </li>
  </ul>

  <ul
    class="cell__column"
    :class="props.class"
    v-else-if="props.class === 'remaining_days'"
  >
    <li v-for="(value, index) in props.content" :key="index" class="column">
      <p class="text" v-if="value < 0">
        Завершилось {{ Math.abs(value) }} дней назад
      </p>
      <p class="text" v-if="value > 0">заканчивается через {{ value }} дней</p>
      <p class="text" v-if="value === 0">заканчивается сегодня {{ value }} дней</p>
    </li>
  </ul>

  <li
    v-else-if="props.class === 'courier_comment'"
    class="cell"
    :class="props.class"
  >
    <p class="text">🚚 {{ props.content }}</p>
  </li>

  <li
    v-else-if="props.class === 'inner_comment'"
    class="cell"
    :class="props.class"
  >
    <p class="text">💬 {{ props.content }}</p>
  </li>

  <li v-else class="cell" :class="props.class">
    <p class="text">{{ props.content }}</p>
  </li>
</template>

<style>

hr {
  width: 100%;
  margin: 4px auto;
  border: 1px dashed rgba(188, 188, 188, 1);
}

.cell {
  box-sizing: border-box;
  width: 100%;
  height: 100%;
  margin: 0 auto;
  padding: 5px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: transparent;
  border-left: 2px solid rgba(222, 226, 230, 1);
 border-right: 2px solid rgba(222, 226, 230, 1);
}

.cell__column {
  box-sizing: border-box;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 5px;
  margin: 0;
  list-style: none;
 border-left: 2px solid rgba(222, 226, 230, 1);
 border-right: 2px solid rgba(222, 226, 230, 1);
}

.text {
  width: 100%;
  margin: 0 auto;
  font-weight: 400;
  font-size: 10px;
  line-height: 16px;
  color: #000000;
}

.client_name p,
.o_id p {
  color: blue;
  font-size: 12px;
}

.diets p{
  font-size: 12px;
}

.cell__column_pay {
  display: flex;
  flex-direction: column;
}

.o_id {
  background-color: rgba(153, 255, 153, 1);
}

.courier_comment {
  justify-content: start;
}

.remaining_days
{
  background-color: rgba(211, 214, 255, 0.6)
}

.pay {
  background-color: rgba(255, 153, 153, 1)
}

.inner_comment {
  box-sizing: border-box;
  padding: 7px;
  background-color: rgba(255, 245, 245, 1);
  border: 1.5px dashed rgba(248, 189, 189, 1);
}

.courier_comment {
  box-sizing: border-box;
  border: 1.5px dashed rgba(224, 203, 234, 1);
}

</style>