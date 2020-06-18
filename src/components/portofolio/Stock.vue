<template>
    <div>
        <div class="card text-white bg-info ml-3 my-3">
            <div class="card-header">{{stock.name}} <small>(Price: {{stock.price}} | Quantity: {{stock.quantity}})</small></div>
            <div class="card-body">
            <h5 class="card-title">Stock Input</h5>
            <div class="float-left">
                <input type="number" class="form-control" :class="{'border border-danger': insufficientQuantity}" placeholder="Quantity" v-model="quantity">
            </div>
            <div class="float-right ml-2">
                <button class="btn btn-danger" @click="sellStock" :disabled="insufficientQuantity || quantity <= 0 || !Number.isInteger(+quantity)">{{insufficientQuantity ? 'Insufficient Quantity' : 'Sell'}}</button>
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
            sellStock(){
                const order = {
                    stockId: this.stock.id,
                    stockPrice: this.stock.price,
                    quantity: this.quantity
                };

                this.$store.dispatch('sellStock', order);
                this.quantity = 0;
            }
        },
        computed: {
            insufficientQuantity() {
                return this.quantity > this.stock.quantity;
            }
        }
    }
</script>

<style>

</style>