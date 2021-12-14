<template>
    <Navbar :logOut="logOut"/>
    
</template>

<script>
import Navbar from './partials/Navbar.vue';

export default {
    name: 'Products',
    components: {
        Navbar
    } ,
    methods: {
        logOut() {
        this.$emit('logout');
        },
    }
}
</script>

<style scoped>
h5{
  text-align-last: center;
  color: blue;
}
div{
    margin-top: 0.5cm;
}
</style>