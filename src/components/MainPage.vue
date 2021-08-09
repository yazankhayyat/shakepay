<template>
    <div>
      <networth-card :data="this.userData"></networth-card>
      <data-table :currentData="this.userData || []"></data-table>
  </div>
</template>

<script>
import axios from 'axios'
import DataTable from './Tables/DataTable.vue'
import NetworthCard from './Cards/NetworthCard.vue'
  export default {
    name: 'MainPage',
    components: {
      DataTable,
      NetworthCard
    },
    data() {
      return {
        userData: []
      }
    },
    mounted() {
     axios
    .get('https://shakepay.github.io/programming-exercise/web/transaction_history.json')
    .then(response => {
      this.userData = response.data
      console.log(this.userData)
    })
    .catch(error => {
      console.log(error)
    })
}
  }
</script>
