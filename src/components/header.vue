<template>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  <div class="container-fluid">
    <router-link to="/" class="navbar-brand">Navbar</router-link>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
      <div class="navbar-nav">
        <router-link to="/" class="nav-link active" aria-current="page">Home</router-link>
        <router-link to="/add" class="nav-link">Add Restaurents</router-link>
      </div>
    </div>
    <div class="d-flex">
        <button v-on:click="logout" class="btn btn-outline-secondary">LogOut</button>
    </div>
  </div>
</nav>
</template>

<script>

export default{
    name:'Header',
    methods:
    {
        logout()
        {
            localStorage.clear();
            this.$router.push({ name: "LogIn" });
        }
    }
}
</script>
