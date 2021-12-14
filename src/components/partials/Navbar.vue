<template>
<nav class="navbar navbar-expand-lg navbar-dark bg-primary">
  <div class="container-fluid">
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNavDropdown">
      <ul class="navbar-nav">
        <li class="nav-item">
          <a class="nav-link active" aria-current="page" href="#">Home</a>
        </li>
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdownMenuLink" role="button" data-bs-toggle="dropdown" aria-expanded="false">
            Clientes
          </a>
          <ul class="dropdown-menu" aria-labelledby="navbarDropdownMenuLink">
            <li><a class="dropdown-item" href="#">Registrar</a></li>
            <li><a class="dropdown-item" href="#">Consultar todos</a></li>
            <li><a class="dropdown-item" href="#">Consultar por ID</a></li>
          </ul>
        </li>
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdownMenuLink" role="button" data-bs-toggle="dropdown" aria-expanded="false">
            Productos
          </a>
          <ul class="dropdown-menu" aria-labelledby="navbarDropdownMenuLink">
            <li><a class="dropdown-item" href="#">Crear</a></li>
            <li><a class="dropdown-item" href="#">Consultar</a></li>
            <li><a class="dropdown-item" href="#">Actualizar</a></li>
            <li><a class="dropdown-item" href="#">Eliminar</a></li>
          </ul>
        </li>
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdownMenuLink" role="button" data-bs-toggle="dropdown" aria-expanded="false">
            Compras
          </a>
          <ul class="dropdown-menu" aria-labelledby="navbarDropdownMenuLink">
            <li><a class="dropdown-item" href="#">Consultar todos</a></li>
            <li><a class="dropdown-item" href="#">Consultar por ID</a></li>
          </ul>
        </li>
        <li class="nav-item dropdown">
          <h5 class="nav-link active dropdown-toggle" href="#" id="navbarDropdownUser" role="button" data-bs-toggle="dropdown" aria-expanded="false"> 
            {{username}}
          </h5>
          <h6 class="dropdown-menu" aria-labelledby="navbarDropdownMenuLink" id="secc">
           <button type="button" @click="logOut()" class="dropdown-item">Cerrar sesión </button> 
          </h6>
        </li>
      </ul>
    </div>
  </div>
</nav>
</template>

<script>

export default {
    name: 'Navbar',
    props: ['logOut'],
    created() {
        this.username = localStorage.getItem('username') || '';
    },
    data() {
        return {
            username: ''
        }
        
    }
    
}
</script>

<style scoped>
h5{
  margin-left: 20cm;
}
h6{
  margin-left: 20cm;
}

</style>