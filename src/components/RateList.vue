<template>
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
        <td>{{ formatNum(key) }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: 'Rates',
  props: ['rates'],
  methods: {
    formatNum(num) {
      return num.toLocaleString('en-US', { minimumFractionDigits: 2, maximumFractionDigits: 2 })
    }
  }
}
</script>