<template>
  <div class="rate-list">
  <table class="rate-list__content table is-striped" >
    <thead>
      <tr>
        <th>Currency</th>
        <th>Rate</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="rate in rates" :key=rate[0]>
        <td>{{ rate[0] }} </td>
        <td>{{ formatNum(rate[1]) }}</td>
      </tr>
    </tbody>
  </table>
  </div>
</template>

<script>
export default {
  name: 'Rates',
  props: ['rates'],
  methods: {
    formatNum(num) {
      return num.toLocaleString('en-US', { minimumFractionDigits: 5, maximumFractionDigits: 5 })
    }
  }
}
</script>

<style>
.rate-list {
  display: flex;
  justify-content: center;

}

.rate-list__content {
  width: 35rem;
}

@media (max-width: 575.98px) {
  .rate-list__content {
    width: 100%;
  }
}
</style>