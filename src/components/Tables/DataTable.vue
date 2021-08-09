<template>
    <vc-table :data="currentData" :rows="rows"  header-cell-classes="border-top-0 bg-secondary">
    </vc-table>
</template>

<script>
import VcTable from './VcTable.vue'

  export default {
    name: 'DataTable',
    components: {
        VcTable
    },
    props: {
        currentData: {
            type: Array,
            required: true
        }
    },
    data() {
        return {
            BTC_RATE: 0,
            ETH_RATE: 0,
            rows: [
                {
                    label: 'Created At',
                    prop: 'createdAt'
                },
                {
                    label: 'Amount',
                    prop: 'amount'
                },
                {
                    label: 'Currency',
                    prop: 'currency'
                }
            ]
        }
    }
  }
</script>

<style lang="scss" scoped></style>
