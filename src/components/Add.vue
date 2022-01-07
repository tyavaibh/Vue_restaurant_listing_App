<template>
    <Header/>
    <h1>Hello {{user_name}}. Welcome to Add Restaurant Page!</h1>

    <form class="add">
        <input type="text" name="name" placeholder="enter restaurant name" v-model="restaurant.name">
        <input type="text" name="contact" placeholder="enter restaurant's contact no." v-model="restaurant.contact">
        <input type="text" name="address" placeholder="enter restaurant's address" v-model="restaurant.address">
        <button type="button" @click="addRestaurant">Add</button>
    </form>
</template>


<script>
import Header from "./Header";
import axios from "axios";

export default {
    name: "Add",

    components:{
        Header
    },

    data(){
        return {
            user_name:"",

            restaurant:{
                name:"",
                contact:"",
                address:""
            }

        }
    },

    methods:{
        async addRestaurant(){
            console.log(this.restaurant);
            let result= await axios.post("http://localhost:3000/restaurants", {
                name:this.restaurant.name,
                contact:this.restaurant.contact,
                address: this.restaurant.address,
            })
            console.log(result.status);

            if(result.status==201){
                this.$router.push({name:'Home'})
            }
        }
    },

    mounted(){
      let user= localStorage.getItem("user-info");
      this.user_name=JSON.parse(user).name;
    }

}
</script>

<style scoped>
h1{
    margin-top:40px;
    margin-bottom: 50px;
}
</style>