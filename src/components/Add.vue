<template>
  <Header />
  <h1>Hello User, Welcome on Add Restaurant Page</h1>
  <form class="add">
    <input
      type="text"
      name="name"
      placeholder="Enter Name"
      v-model="Restaurant.name"
    />
    <input
      type="text"
      name="address"
      placeholder="Enter Address"
      v-model="Restaurant.address"
    />
    <input
      type="text"
      name="contact"
      placeholder="Enter Contact"
      v-model="Restaurant.contact"
    />
    <button v-on:click="addRestaurant" type="button">Add new Restaurant</button>
  </form>
</template>
<script>
import Header from "./Header.vue";
import axios from "axios";
export default {
  name: "Add",
  components: {
    Header,
  },
  data() {
    return {
      Restaurant: {
        name: "",
        address: "",
        contact: "",
      },
    };
  },
  methods: {
   async addRestaurant() {

      const result =await axios.post("http://localhost:3000/restsurant",{
        name:this.Restaurant.name,
        address:this.Restaurant.address,
        contact:this.Restaurant.contact,
      })
      if(result.status == 201)
      {
        this.$router.push({
          name:"Home"
        })
      }
      // console.warn("result",result)
    },
  },
  mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "Login" });
    }
  },
};
</script>
