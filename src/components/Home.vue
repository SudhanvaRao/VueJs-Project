<template>
  <Header />
  <h1 class="m-5">Hello {{name}}, Welcome to Home Page</h1>

  <div class="container mt-3">
    <table class="table table-bordered border-secondary text-center">
    <thead class="table-dark">
      <tr>
        <th scope="col">ID</th>
        <th scope="col">Restaurant Name</th>
        <th scope="col">Contact Number</th>
        <th scope="col">Adderss</th>
        <th scope="col">Update</th>
        <th scope="col">Delete</th>
    </tr>
  </thead>
    <tbody>
      <tr v-for="item in user_resto" :key="item.id">
          <th scope="row">{{item.id}}</th>
          <td>{{item.name}}</td>
          <td>{{item.contact}}</td>
          <td>{{item.address}}</td>
          <td>
            <router-link :to="'/update/'+ item.id" >
            <button class="btn btn-outline-primary">Update</button>
            </router-link>
          </td>
          <td><button v-on:click="delResto(item.id)" class="btn btn-outline-danger">Delete</button></td>
      </tr>
    </tbody>
</table>
  </div>
</template>

<script>
import Header from "./header.vue";
import axios from 'axios';
export default {
  components: {
   Header,
  },
  name: "Home",
  data()
  {
      return {
        name:"",
        user_id:"",
        restaurants:[],
      }
  },
  async mounted() {
    this.loadData();
  },
  methods:{
    async delResto(id)
    {
        let r = await axios.get("http://localhost:3000/restaurant/"+id)
        if(this.user_id == r.data.user_id)
        {
          let result = await axios.delete('http://localhost:3000/restaurant/'+id)
          if(result.status==200)
          {
              this.loadData();
          }
        }
    },
    async loadData()
    {
      let user = localStorage.getItem('user-info');

      if (!user) {
          this.$router.push({ name: "SignUp" });
      }
      else{
        this.name = JSON.parse(user).name;
        this.user_id = JSON.parse(user).id;
        console.log(this.user_id)
        let result = await axios.get('http://localhost:3000/restaurant')
        this.restaurants = result.data;
      }

    }
  },
  computed:{
    user_resto: function()
    {
      return this.restaurants.filter(function(u){

        let user = localStorage.getItem('user-info');

        return u.user_id == JSON.parse(user).id
      })
    }
  },
  
};
</script>
