<template>
  <div id='app'>
    <Header />
    <ExchangeRates />
  </div>
</template>

<script>
import ExchangeRates from './components/ExchangeRates.vue'
import Header from './components/Header.vue'

export default {
  name: 'app',
  components: {
    ExchangeRates,
    Header
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
