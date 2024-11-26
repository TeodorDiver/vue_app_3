<template>
  <div id="app">
    <CurrencyDisplay />
  </div>
</template>

<script>
import CurrencyDisplay from './components/CurrencyDisplay.vue';

export default {
  components: {
    CurrencyDisplay,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
