<template>
  <div class='exchange-rates'>
    <div v-if='rates.length === 0'>
      <span class='loader is-size-2' />
    </div>
    <div v-else>
      <h1 class='title'>New Zealand Dollar<br>Foreign Exchange Rates: {{ date }}</h1>
      <text-filter @searchData="getSearch" />
      <rate-list v-bind:rates="filteredList" />
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import RateList from './RateList.vue'
import TextFilter from './TextFilter.vue'

const URL = 'https://api.exchangerate.host/latest?base=NZD'

export default {
  name: 'exchange-rates',
  components: {
    RateList,
    TextFilter
  },
  data: () => ({
    date: [],
    rates: [],
    errors: [],
    searchText: ''
  }),
  mounted() {
    this.fetchData()
  },
  computed: {
    filteredList: function() {
      const filteredRates = {}
      const list = this.rates
      Object.keys(list).filter((item) => {
        return (
          (item !== 'NZD')
          && item.includes(this.searchText.toUpperCase())
        )
      })
      .forEach(function(key) {
          filteredRates[key] = list[key]
        });
        return filteredRates
    }
  },
  methods: {
    fetchData() {
      axios
        .get(URL)
        .then(response => {
          this.rates = response.data.rates
          this.date = response.data.date
        })
        .catch(error => this.errors.push(error))
    },
    getSearch: function(txt) {
      this.searchText = txt
    }
  }
}
</script>

<style scoped>
h1 {
  margin: 1rem 0;
}
a {
  color: #42b983;
}
.exchange-rates {
  display: flex;
  flex: 1;
  align-items: flex-start;
  justify-content: center;
}
.table {
  width: 70%;
  margin: 0 auto;
}

@media (max-width: 575.98px) {
  .table {
    width: 90%;
  }
}
</style>
