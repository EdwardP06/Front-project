<template>
    <Navbar :logOut="logOut"/>
     <div class="container mt-14">
        <div class="row">
            <div class="col-12">
                <h1>Registro de productos</h1>
                <label for="name_product" >Nombre del producto</label>
                <div>
                    <InputText 
                    id="name_product" 
                    type="text" 
                    v-model="name_product"/>
                </div>
            </div>
            <div class="col-12">
                <label for="price" >Precio</label>
                <div>
                    <InputText 
                    id="price" 
                    type="float " 
                    v-model="price"/>
                </div>
            </div>
            <div class="col-12">
                <label for="description">Descripción</label>
                <div>
                    <InputText 
                    id="description" 
                    type="text" 
                    v-model="description"/>
                </div>
            </div>
            <div class="col-12">
                <label for="size">Talla</label>
                <div>
                    <InputText 
                    id="size" 
                    type="text" 
                    v-model="size"/>
                </div>
            </div>
        </div>
        <button type="button" @click="Save()" class="btn btn-primary btn-lg">Guardar </button>
        <button type="button" v-on:click="goToHome()" class="btn btn-primary btn-lg">Cancelar</button>
    </div>
    
</template>

<script>
import gql from "graphql-tag";
import Navbar from './partials/Navbar.vue';
import InputText from 'primevue/inputtext';

export default {
    name: 'Products',
    components: {
        Navbar,
        InputText
    } ,
    data() {
        return {
            name: '',
            price: '',
            description: '',
            size: ''
        }
    },
    methods: {
        logOut() {
        this.$emit('logout');
        },
        Save() {
            this.$apollo.mutate({
                mutation: gql`
                    mutation ProductDetail(
                        $name: String!, 
                        $price: Float!, 
                        $description: String!, 
                        $image: String!, 
                        $size: String!) {
                            ProductDetail(
                                name: $name, 
                                price: $price, 
                                description: $description, 
                                image: $image, 
                                size: $size) {
                                    name
                                    price
                                    description
                                    size
                                    }
                        }
                    `,
                variables: {
                    name: this.name,
                    price: this.price,
                    description: this.description,
                    size: this.size,
                }   
            }
        )},
        goToHome() {
            this.$router.push({ name: 'home' });
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

<style scoped>

.row{
    margin-top: 0cm;
    margin-left: 5cm;
    width: 35cm;
    height: 12cm;
   
}
h1{
    margin-bottom: 0.4cm;
    margin-top: 0.1;

}
label{
    margin: 0.3cm;
    margin-top: 0cm;
    margin-bottom: 0cm;
    width: 50%;
}
button{
    margin: 0.7cm;
    margin-left: 7.3cm;   
    
}
.p-inputtext {
    height: 0.7cm;
    width: 55%;
}
</style>