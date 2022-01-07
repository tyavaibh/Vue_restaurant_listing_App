<template>
  <img class="logo" src="../assets/restro-logo-2.png" alt="Restaurant Logo" />
  <h1>Login!</h1>
  <div class="login">
    <input type="text" placeholder="enter your email" v-model="email" />
    <input type="text" placeholder="enter your password" v-model="password" />

    <button @click="Login">Login!</button>

    <p>
      <router-link to="/sign-up">Sign Up!</router-link>
    </p>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Login",

  data() {
    return {
      email: "",
      password: "",
    };
  },

  methods: {
    async Login() {

      let result = await axios.get(
        `http://localhost:3000/users?email=${this.email}&password=${this.password}`
      );
      console.log(result.data);

      if (result.status == 200 && result.data.length) {
        localStorage.setItem("user-info", JSON.stringify(result.data[0]));
        this.$router.push({ name: "Home" }); //statement responsible for re-directing
      }else{
        alert("Invalid Credentials! Please try again.")
      }
    },
  },

  mounted(){
      let user= localStorage.getItem("user-info");
      if(user){
          this.$router.push({name:'Home'}) //statement responsible for re-directing
      }
  }
};
</script>
