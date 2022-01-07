<template>
  <Header />
  <h1>Hello {{ name }}. Welcome to your Home Page!</h1>
  <br />
  <table border="1">
    <thead>
      <th>S. No.</th>
      <th>Name</th>
      <th>Contact</th>
      <th>Address</th>
      <th>Action</th>
    </thead>

    <tr v-for="restaurant in restaurants" :key="restaurant.id">
      <td>{{ restaurant.id }}</td>
      <td>{{ restaurant.name }}</td>
      <td>{{ restaurant.contact }}</td>
      <td>{{ restaurant.address }}</td>
      <td>
        <router-link class="route" :to="'/update/' + restaurant.id"
          >Update</router-link
        >
        <button class="btn" @click="deleteRestaurant(restaurant.id)">
          Delete
        </button>
      </td>
    </tr>
  </table>
</template>

<script>
import Header from "./Header";
import axios from "axios";

export default {
  name: "Home",

  components: {
    Header,
  },

  data() {
    return {
      name: "",
      restaurants: [],
    };
  },

  methods: {

    async deleteRestaurant(id) {
      let result = await axios.delete(
        "http://localhost:3000/restaurants/" + id
      );

      if (result.status == 200) {
        this.loadPage();
      }
    },

    async loadPage() {
      let user = localStorage.getItem("user-info");
      this.name = JSON.parse(user).name;

      if (!user) {
        this.$router.push({ name: "SignUp" }); //statement responsible for re-directing
      }

      let result = await axios.get("http://localhost:3000/restaurants");
      this.restaurants = result.data;
    },
  },

  async mounted() {
    let user = localStorage.getItem("user-info");
    console.warn(user);

    try {
        this.name = JSON.parse(user).name;
    }

    catch(err) {
       console.log(err)
    }

    if (!user) {
      this.$router.push({ name: "SignUp" }); //statement responsible for re-directing
    }

    let result = await axios.get("http://localhost:3000/restaurants");
    console.log(result.status)
    this.restaurants = result.data;
  },
};
</script>

<style scoped>
td,
thead {
  width: 150px;
  height: 40px;
}

table {
  margin: auto;
}

.route {
  text-decoration: none;
  background-color: green;
  color: white;
  padding: 5px;
  border-radius: 5px;
  margin-right: 10px;
}

.btn {
  background-color: rgb(226, 19, 19);
  color: white;
  padding: 5px;
  border-radius: 5px;
  border: none;
  padding: 5px;
  font-size: 17px;
}
</style>
