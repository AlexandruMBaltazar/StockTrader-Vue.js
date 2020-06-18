<template>
    <div class="container">
        <app-header></app-header>
        <transition
            enter-active-class="animate__animated animate__backInLeft"
            leave-active-class="animate__animated animate__backOutRight"
            mode="out-in"
        >
            <router-view></router-view>
        </transition>
    </div>
</template>

<script>
    import Header from './components/Header.vue'

    export default {
        components: {
            appHeader: Header
        },
        created() {
            this.$store.dispatch('initStocks');
        }
    }
</script>

<style>
    body{
        padding: 30px;
    }
</style>
