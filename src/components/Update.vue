<template>
  <Header />
  <img class="logo mt-5" alt="Food logo" src="../assets/img/LogoFood.png" />
  <h1 class="mt-5">Hello {{this.name}}, Welcome to Update Page</h1>

  <div class ="mt-5 container form-group col-5">
    <div class="mb-3">
        <input type="text" class="form-control" v-model="restaurant.name" placeholder="Restaurant Name"/>
    </div>
    <div class="mb-3">
        <input type="text" class="form-control" v-model="restaurant.address" placeholder="Address"/>
    </div>
    <div class="mb-3">
        <input type="text" class="form-control" v-model="restaurant.contact" placeholder="Contact Number"/>
    </div>
    <div class="d-grid gap-2 col-5 mx-auto">
        <button v-on:click="update" class="btn btn-primary mt-3">Update Restaurant</button>
    </div>
</div>

</template>

<script>
import Header from "./header.vue";
import axios from 'axios'
export default {
  name: "Update",

  data(){

    return{
      name:'',
      restaurant :{
                user_id:'',
                name:'',
                address:'',
                contact:''
            }
    }

  },
  
  components: {
   Header,
  },
  async mounted(){
        let user = localStorage.getItem('user-info')
        if(!user)
        {
            this.$router.push({ name: "SignUp" });
        }
        this.name = JSON.parse(user).name;
        let result = await axios.get("http://localhost:3000/restaurant/"+this.$route.params.id)
        console.log(this.$route.params.id)
        this.restaurant = result.data 
    },
    methods: {
      async update()
      {
          console.warn(this.restaurant)
            let result =  await axios.put("http://localhost:3000/restaurant/"+this.$route.params.id, {
              name: this.restaurant.name,
              address: this.restaurant.address,
              contact: this.restaurant.contact,
              user_id: this.restaurant.user_id
            });
            console.log(this.$route.params.id)
            console.log(result.status)
            if(result.status==200)
            {
                this.$router.push({ name: "Home" });
            }
      }
    }
};
</script>
