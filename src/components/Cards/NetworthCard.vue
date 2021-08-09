<template>
    <el-card class="box-card">
        <div slot="header" class="clearfix">
            <div class="col">
                <h5 class="text-uppercase text-muted ls-1 m-0">NET WORTH</h5>
            </div>
        </div>
        <h4 class="text-muted my-5">Current Networth: {{ findNetworth }}</h4>
    </el-card>
</template>

<script>
import { ElCard } from 'element-ui'
export default {
    components: {
        'el-card': ElCard,
    },
    data() {
        return {
            BTC_RATE: 57503.04,
            ETH_RATE: 3926.87
        }
    },
    props: {
        data: {
            type: Array,
            required: true
        }
    },
    computed: {
        findNetworth() {
            let btcBalance = 0
            let ethBalance = 0
            let cadBalance = 0
            this.data.forEach((x) => {
                if (x.currency === 'BTC') {
                    if (x.direction === 'debit') {
                        btcBalance = btcBalance - x.amount
                    } else {
                        btcBalance += x.amount
                    }
                } else if (x.currency === 'ETH') {
                    if (x.direction === 'debit') {
                        ethBalance = ethBalance - x.amount
                    } else {
                        ethBalance += x.amount
                    }                
                } else if (x.currency === 'CAD') {
                     if (x.direction === 'debit') {
                        cadBalance = cadBalance - x.amount
                    } else {
                        cadBalance += x.amount
                    }  
                }
            })
            var formatter = new Intl.NumberFormat('en-US', {
                style: 'currency',
                currency: 'CAD'
            })
            return formatter.format(cadBalance + (btcBalance * this.BTC_RATE) + (ethBalance * this.ETH_RATE))
        }
    }
}
</script>
