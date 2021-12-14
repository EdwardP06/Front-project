<template>
    <div class="container mt-5">
        <div class="row mb-3">
            <div class="col-4">
                <h1>Inicio de sesión</h1>
                <label for="username" >Nombre de usuario</label>
                <div>
                    <InputText 
                    id="username" 
                    type="text" 
                    v-model="username"/>
                </div>
            </div>
        </div>
        <div class="row mb-3">
            <div class="col-4">
                <label for="password">Contraseña</label>
                <div>
                    <InputText 
                    id="password" 
                    type="password" 
                    v-model="password"/>
                </div>
            </div>
        </div>
        <button type="button" @click="signIn()" class="btn btn-primary btn-lg">iniciar sesión </button>
        <button type="button" v-on:click="goToSignUp()" class="btn btn-link">¿No tienes usuario? ¡Regístrate!</button>
       
        
        
    </div>
    
</template>

<script>
import gql from "graphql-tag";
import InputText from 'primevue/inputtext';


export default {
    name: 'SignIn',
    components: {
        InputText,
        
    },
    created() {
        localStorage.clear();
    },
    data() {
        return {
            username: '',
            password: ''
        }
    },
    methods: {
        signIn() {
            this.$apollo.mutate({
                mutation: gql`
                    mutation ($username: String!, $password: String!) {
                        login(username: $username, password: $password) {
                            access
                            refresh
                        }
                    }
                `,
                variables: {
                    username: this.username,
                    password: this.password
                }
            }).then(response => {
                this.$emit('login', {
                    access_token: response.data.login.access,
                    refresh_token: response.data.login.refresh,
                    username: this.username
                });
            }).catch(e => {
                console.log(JSON.stringify(e, null, 2));
            });
        },
        goToSignUp() {
            this.$router.push({ name: 'signUp' });
        }
    }
}
</script>

<style scoped>

h1{
    margin-top: 2cm;
    margin-bottom: 1cm;
}
.row{
    margin-top: 0.5cm;
    margin-inline: 5cm;
    width: 59cm;
}
button{
    margin: 0.7cm;
    margin-left: 6.5cm;
}
.p-inputtext {
    height: 1cm;
    width: 100%;
    margin: 0.1cm;
    
}
</style>