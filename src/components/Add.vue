<template>
  <Header />
  <img class="logo mt-5" alt="Food logo" src="../assets/img/LogoFood.png" />
  <h1 class="mt-5">Hello {{this.name}}, this is Add Restaurant Page</h1>

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
        <button v-on:click="Add" class="btn btn-primary mt-3">Add New Restaurants</button>
    </div>
</div>

</template>

<script>
import Header from "./header.vue";
import axios from "axios";
export default {
    name: "Add",
    components: {
        Header,
    },
    data() 
    {
        return {
            name:'',
            restaurant :{
                user_id:'',
                name:'',
                address:'',
                contact:''
            }
        }
    },
    mounted(){
        let user = localStorage.getItem('user-info')
        
        this.name = JSON.parse(user).name;
        if(!user)
        {
            this.$router.push({ name: "SignUp" });
        }
        this.restaurant.user_id = JSON.parse(user).id
    },
    methods:{
        async Add()
        {
            console.warn(this.restaurant)
            let result =  await axios.post("http://localhost:3000/restaurant", {
            name: this.restaurant.name,
            address: this.restaurant.address,
            contact: this.restaurant.contact,
            user_id: this.restaurant.user_id
            });
            
            if(result.status==201)
            {
                this.$router.push({ name: "Home" });
            }
            
        },
    },
};
</script>
