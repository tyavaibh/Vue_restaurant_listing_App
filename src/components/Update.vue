<template>
    <Header/>
    <h1>Hello {{name}}. Welcome to Update Restaurant Page!</h1>

     <form class="update">
        <input type="text" name="name" placeholder="enter restaurant name" v-model="restaurant.name">
        <input type="text" name="contact" placeholder="enter restaurant's contact no." v-model="restaurant.contact">
        <input type="text" name="address" placeholder="enter restaurant's address" v-model="restaurant.address">
        <button type="button" @click="updateRestaurant">Update</button>
    </form>
</template>


<script>
import Header from "./Header";
import axios from "axios";

export default {
    name: "Update",

    components:{
        Header
    },

    data(){
        return {
            name:"",

            restaurant:{
                name:"",
                contact:"",
                address:""
            }
        }
    },

    methods:{
        async updateRestaurant(){
            let result= await axios.put("http://localhost:3000/restaurants/"+ this.$route.params.id , {
                name:this.restaurant.name,
                contact:this.restaurant.contact,
                address: this.restaurant.address,
            })
            console.log(result.status);

            if(result.status==200){
                this.$router.push({name:'Home'})
            }
        }
    },

    async mounted(){
      let user= localStorage.getItem("user-info");
      this.name=JSON.parse(user).name;
      console.log(user);

      let result= await axios.get('http://localhost:3000/restaurants/' + this.$route.params.id);
      this.restaurant=result.data;

    }

}
</script>
