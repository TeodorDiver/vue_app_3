<template>
  <div>
    <h1>Курс валют</h1>
    <p>Курс рубля к доллару: {{ rates.USD }} ₽</p>
    <p>Курс рубля к евро: {{ rates.EUR }} ₽</p>
    <p>Текущая дата и время: {{ currentDate }}</p>
    <button @click="fetchRates">Обновить</button>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      rates: {
        USD: null,
        EUR: null,
      },
      currentDate: new Date().toLocaleString('ru-RU'),
    };
  },
  methods: {
    async fetchRates() {
  try {
    const response = await axios.get('/api/scripts/XML_daily.asp'); // Используйте относительный путь
    const parser = new DOMParser();
    const xml = parser.parseFromString(response.data, 'text/xml');

    this.rates.USD = xml.querySelector('Valute[ID="R01235"] > Value').textContent;
    this.rates.EUR = xml.querySelector('Valute[ID="R01239"] > Value').textContent;

    this.currentDate = new Date().toLocaleString('ru-RU');
  } catch (error) {
    console.error('Ошибка при получении данных:', error);
  }
},
  },
  created() {
  this.fetchRates(); // Запрашиваем данные сразу при создании компонента
  setInterval(() => {
    this.currentDate = new Date().toLocaleString('ru-RU');
  }, 1000); // Обновляем дату каждую секунду
},
};
</script>

<style scoped>
/* Добавьте стили по вашему усмотрению */
</style>