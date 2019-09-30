<template>
  <div id='app'>
    <Header />
    <ExchangeRates />
    <Footer />
  </div>
</template>

<script>
import ExchangeRates from './components/ExchangeRates.vue'
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'app',
  components: {
    ExchangeRates,
    Header,
    Footer
  },
  created() {
    document.title = 'Exchange Rates'
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
  display: flex;
  flex-direction: column;
  height: 100vh;
}
</style>
