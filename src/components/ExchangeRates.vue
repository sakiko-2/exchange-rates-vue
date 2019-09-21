<template>
  <div class='exchange-rates'>
    <h1 class='title'>New Zealand Dollar<br>Foreign Exchange Rates: {{ date }}</h1>
    <table class='table is-striped' >
      <thead>
        <tr>
          <th>Currency</th>
          <th>Rate</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for='(key, value) in rates' :key=value >
          <td>{{ value }} </td>
          <td>{{ key.toLocaleString('en-US', { minimumFractionDigits: 2, maximumFractionDigits: 2 }) }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';

const URL = 'https://api.exchangeratesapi.io/latest?base=NZD';

export default {
  name: 'exchange-rates',
  data: () => ({
    date: [],
    rates: [],
    errors: []
  }),
  mounted() {
    this.fetchData()
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
    }
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.table {
  width: 50%;
  margin: 0 auto;
}

@media (max-width: 575.98px) {
  .table {
    width: 90%;
  }
}
</style>
