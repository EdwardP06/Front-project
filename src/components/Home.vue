<template>
    <Navbar :logOut="logOut"/>
    <div class="container mt-5">
    <div class="row row-cols-1 row-cols-md-3 g-4">
        <div class="col">
            <div class="card border-primary mb-3" style="width: 18rem;">
            <img v-on:click="goToClients()" src="https://thumbs.dreamstime.com/b/icono-s%C3%B3lido-negro-para-los-clientes-la-gente-y-el-equipo-logotipo-s%C3%ADmbolo-146530412.jpg" class="card-img-top" alt="..." >
            <div class="card-body">
                <h5 class="card-title">Clientes</h5>
            </div>
            </div>
        </div>
        <div class="col">
            <div class="card border-primary mb-3" style="width: 18rem;">
            <img v-on:click="goToProducts()"  src="data:image/png;base64,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" class="card-img-top" alt="...">
            <div class="card-body">
                <h5 class="card-title">Productos</h5>
            </div>
            </div>
        </div>
        <div class="col">
            <div class="card border-primary mb-3" style="width: 18rem;">
            <img v-on:click="goToPurchases()" src="https://th.bing.com/th/id/R.3f76ae744faad725b3d704365b5fd12b?rik=pxDv4zuVlsqOvQ&riu=http%3a%2f%2fclipart-library.com%2fnew_gallery%2f101-1016675_shopping-bags-png.png&ehk=si%2bOv7eZlPL2zXWsTb0KSzkJTv8wukMyUoNtfrTQJUY%3d&risl=&pid=ImgRaw&r=0" class="card-img-top" alt="..." height="285">
            <div class="card-body">
                <h5 class="card-title">Compras</h5>
            </div>
            </div>
        </div>
    </div>
    </div>
</template>

<script>
import Navbar from './partials/Navbar.vue';

export default {
    name: 'Home',
    components: {
        Navbar
    } ,
    methods: {
        logOut() {
        this.$emit('logout');
        },
        goToProducts() {
            this.$router.push({ name: 'Products' });
        },
        goToClients() {
            this.$router.push({ name: 'Clients' });
        },
        goToPurchases() {
            this.$router.push({ name: 'Purchases' });
        }
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