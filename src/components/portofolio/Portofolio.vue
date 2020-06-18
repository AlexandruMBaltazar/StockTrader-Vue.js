<template>
    <div>
        <app-stock v-for="stock in stocks" :stock="stock"></app-stock>
    </div>
</template>

<script>
    import Stock from './Stock.vue'

    export default {
        computed: {
            stocks(){
                return this.$store.getters.stockPortofolio;
            }
        },
        components: {
            appStock: Stock
        }
    }
</script>

<style scoped>
    div{
        display: inline-block;
    }
</style>