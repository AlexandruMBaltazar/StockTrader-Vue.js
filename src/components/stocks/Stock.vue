<template>
    <div>
        <div class="card bg-light ml-3 my-3">
            <div class="card-header">{{stock.name}} <small>(Price: {{stock.price}})</small></div>
            <div class="card-body">
            <h5 class="card-title">Stock Input</h5>
            <div class="float-left">
                <input type="number" class="form-control" :class="{'border border-danger': insufficientFunds}" placeholder="Quantity" v-model="quantity">
            </div>
            <div class="float-right ml-2">
                <button class="btn btn-success" @click="buyStock" :disabled="insufficientFunds || quantity <= 0 || !Number.isInteger(+quantity)">{{ insufficientFunds ? 'Insufficient Funds' : 'Buy'}}</button>
            </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: ["stock"],
        data(){
            return{
                quantity: 0
            }
        },
        methods: {
            buyStock(){
                const order = {
                    stockId: this.stock.id,
                    stockPrice: this.stock.price,
                    quantity: this.quantity
                };
                this.$store.dispatch('buyStock', order);
                this.quantity = 0;
            }
        },
        computed: {
            funds(){
                return this.$store.getters.funds;
            },
            insufficientFunds(){
                return this.quantity * this.stock.price > this.funds;
            }
        }
    }
</script>
