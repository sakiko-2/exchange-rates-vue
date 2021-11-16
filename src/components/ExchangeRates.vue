<template>
  <div class="exchange-rates section">
    <div v-if='rates.length === 0'>
      <span class="loader is-size-2" />
    </div>
    <div v-else>
      <h1 class="subtitle is-3">New Zealand Dollar<br>Foreign Exchange Rates: {{ date }}</h1>
      <text-filter @searchData="getSearch" />
      <sort-dropdown v-bind:sortBy="sortBy" @sortKey="getSortBy" />
      <rate-list v-bind:rates="filteredList" />
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import RateList from './RateList.vue'
import TextFilter from './TextFilter.vue'
import SortDropdown from './SortDropdown.vue'

const URL = 'https://api.exchangerate.host/latest?base=NZD'

export default {
  name: 'exchange-rates',
  components: {
    RateList,
    TextFilter,
    SortDropdown
  },
  data: () => ({
    date: [],
    rates: [],
    errors: [],
    searchText: '',
    sortBy: 'currency'
  }),
  mounted() {
    this.fetchData()
  },
  computed: {
    filteredList: function() {
      return Object.entries(this.rates)
        .filter((item) => {
          return (
            (item[0] !== 'NZD')
            && item[0].includes(this.searchText.toUpperCase())
          )
        })
        .sort((a, b) => {
          if (this.sortBy === 'rate') {
            return a[1] > b[1] ? 1 : -1
          }
          return a[0] > b[0] ? 1 : -1
        })
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
    },
    getSortBy: function(item) {
      this.sortBy = item
    }
  }
}
</script>

<style scoped>
.exchange-rates {
  display: flex;
  flex: 1;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
}
</style>
