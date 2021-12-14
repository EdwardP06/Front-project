<template>
    <div class="container mt-5">
        <div class="row">
            <div class="col-12">
                <h1>Registro de usuario</h1>
                <label for="name" >Nombre</label>
                <div>
                    <InputText 
                    id="name" 
                    type="text" 
                    v-model="name"/>
                </div>
            </div>
            <div class="col-120">
                <label for="username" >Nombre de usuario</label>
                <div>
                    <InputText 
                    id="username" 
                    type="text" 
                    v-model="username"/>
                </div>
            </div>
            <div class="col-12">
                <label for="email">Correo electrónico</label>
                <div>
                    <InputText 
                    id="email" 
                    type="email" 
                    v-model="email"/>
                </div>
            </div>
            <div class="col-12">
                <label for="password">Contraseña</label>
                <div>
                    <InputText 
                    id="password" 
                    type="password" 
                    v-model="password"/>
                </div>
            </div>
        </div>
        <button type="button" @click="signUp()" class="btn btn-primary btn-lg">Registrarme </button>
        <button type="button" v-on:click="goToSignIn()" class="btn btn-link">¿Tienes usuario? ¡Inicia sesión!</button>
    </div>
</template>

<script>
import gql from "graphql-tag";
import Swal from "sweetalert2";
import InputText from 'primevue/inputtext';


export default {
    name: 'SignUp',
    components: {
        InputText,
       
    },
    data() {
        return {
            username: '',
            name: '',
            email: '',
            password: ''
        }
    },
    methods: {
        signUp() {
            Swal.fire({
                title: 'Creando usuario',
                html: 'Espera un momento mientras creamos tu cuenta...',
                allowOutsideClick: false,
                didOpen: () => {
                    Swal.showLoading();
                }   
            });
            this.$apollo.mutate({
                mutation: gql`
                    mutation newUser(
                        $username: String!, 
                        $password: String!, 
                        $name: String!, 
                        $email: String!) {
                            newUser(
                                username: $username, 
                                password: $password, 
                                name: $name, 
                                email: $email) {
                                    username
                                    password
                                    name
                                    email
                                }
                        }
                    
                `,
                variables: {
                    username: this.username,
                    password: this.password,
                    name: this.name,
                    email: this.email,
                    
                }
            }).then(response => {
                Swal.close();
                Swal.fire(
                'Usuario creado',
                `El usuario ${response.data.newUser.username} ha sido creado satisfactoriamente`,
                'success'
                )
                this.goToSignIn();
            }).catch(e => {
                Swal.close();
                console.log(JSON.stringify(e, null, 2));
            });
        },
        goToSignIn() {
            this.$router.push({ name: 'signIn' });
        }
    }
}
</script>

<style scoped>

.row{
    margin-top: 0cm;
    margin-left: 5cm;
    width: 35cm;
   
}
h1{
    margin-bottom: 0.4cm;
    margin-top: 0.2;
}
label{
    margin: 0.3cm;
    margin-top: 0cm;
    margin-bottom: 0cm;
    width: 50%;
}
button{
    margin: 0.7cm;
    margin-left: 6.5cm;   
    
}
.p-inputtext {
    height: 1cm;
    width: 55%;
    margin: 0.3cm;
    margin-bottom: 0cm;
    
    
}
</style>