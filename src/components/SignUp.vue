<template>
  <img class="logo" alt="Food logo" src="../assets/img/LogoFood.png" />
  <h1>SignUp</h1>

  <div class="container form-group col-3">
    <input class="form-control mt-3" type="text" v-model="name" placeholder="Enter Name"/>
    <input class="form-control mt-3" type="text" v-model="email" placeholder="Enter Email"/>
    <input class="form-control mt-3" type="password" v-model="password" placeholder="Enter Password"/>

    <div class="d-grid gap-2 col-4 mx-auto">
      <button v-on:click="signup" class="btn btn-primary mt-3">SignUp</button>
    </div>
    <div class="mt-2">
      <router-link to="/log-in">LogIn</router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "SignUp",
  data() {
    return {
      name: "",
      email: "",
      password: "",
    };
  },
  components: {},
  async mounted() {
    let user = localStorage.getItem("user-info");
    if (user) {
      this.$router.push({ name: "Home" });
    }
  },
  methods: {
    async signup() {
      let result = await axios.post("http://localhost:3000/user", {
        name: this.name,
        password: this.password,
        email: this.email,
      });

      if (result.status == 201) {
        localStorage.setItem("user", JSON.stringify(result.data));
        this.$router.push({ name: "Home" });
      }
    },
  },
};
</script>

<style>
.logo {
  width: 200px;
}
</style>