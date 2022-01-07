<template>

    <img class="logo" src="../assets/restro-logo-2.png" alt="Restaurant Logo">
    <h1>Sign Up!</h1>
    <div class="register">
    <input type="text" placeholder="enter your name" v-model="name">
    <input type="text" placeholder="enter your email" v-model="email">
    <input type="text" placeholder="enter your password" v-model="password">

    <button @click="SignUp">Sign Up!</button>

    <p>
        <router-link to="/login">Login!</router-link>
    </p>
  </div>
</template>


<script>
import axios from "axios";


export default {
    name: "SignUp",

    data(){
    return {
      name:"",
      email: "",
      password: ""
    }
  },

  methods: {
    async SignUp(){
      let result= await axios.post("http://localhost:3000/users", {
        name:this.name, 
        email:this.email,
        password:this.password})

      console.log(result);

      if(result.status==201){

      //  ------CHANGED CODE LINE-------

      //  localStorage.setItem("user-info",JSON.stringify(result.data));
       this.$router.push({name:'Login'}) //statement responsible for re-directing
      }
    }
  },

  mounted(){
      let user= localStorage.getItem("user-info");
      if(user){
          this.$router.push({name:'Home'}) //statement responsible for re-directing
      }
  }
}
</script>

