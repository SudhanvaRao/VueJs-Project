<template>
  <Header />
  <img class="logo mt-3" alt="Food logo" src="../assets/img/LogoFood.png" />
  <h1>Log-in</h1>

  <div class="container form-group col-3">
    <input class="form-control mt-3" type="text" v-model="email" placeholder="Enter Email"/>
    <input class="form-control mt-3" type="text" v-model="password" placeholder="Enter Password"/>

    <div class="d-grid gap-2 col-4 mx-auto">
      <button v-on:click="login" class="btn btn-primary mt-3">Login</button>
    </div>
    <div class="mt-2">
      <router-link to="/sign-up">Don't have an account?</router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Header from './header.vue';
export default {
  components: { Header },
  name: "LogIn",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  async mounted() {
    let user = localStorage.getItem('user-info');
    if (user) {
      this.$router.push({ name: "Home" });
    }
  },
  methods: {
    async login() {
      let result = await axios.get(
        `http://localhost:3000/user?email=${this.email}&password=${this.password}`
      );
      // console.log(result);
      if (result.status == 200 && result.data.length > 0) {
        console.log(result.status)
        localStorage.setItem("user-info", JSON.stringify(result.data[0]));
        this.$router.push({ name: "Home" });
      }
    },
  },
};
</script>
