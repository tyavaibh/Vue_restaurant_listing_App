<template>
    <div class="nav">
        <router-link to="/">Home</router-link>
        <router-link to="/add">Add Restaurant</router-link>
        <router-link to="#" @click="logout">Logout!</router-link>
    </div>
</template>

<script>

export default {
    name:'Header',

    methods:{
        logout(){
            localStorage.clear();
            this.$router.push({name:'Login'})
        }
    }
}
</script>


<style> 
    .nav{
        background-color:#333;
        overflow: hidden;
    }

    .nav a{
        float: left;
        color: white;
        padding: 14px 16px;
        font-size: 17px;
        text-decoration: none;
        margin-right: 5px;
        text-align: center; 
    }

    .nav a:hover {
        background-color:#ddd;
        color: #333;
    }
</style>