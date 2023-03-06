<template>
  <Header />
  <h1>Hello User, Welcome on Update Restaurant Page</h1>
  <form class="update">
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
    <button v-on:click="updateRestaurant" type="button">
      Update Restaurant
    </button>
  </form>
</template>
<script>
import Header from "./Header.vue";
import axios from "axios";
export default {
  name: "Update",
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
  async mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "Login" });
    }
    const result = await axios.get(
      "http://localhost:3000/restsurant/" + this.$route.params.id
    );
    // console.warn(this.$route.params.id)
    // console.warn(result.data)
    this.Restaurant = result.data;
  },
  methods: {
    async updateRestaurant() {
      console.warn(this.Restaurant);
      const result = await axios.put(
        "http://localhost:3000/restsurant/" + this.$route.params.id,
        {
          name: this.Restaurant.name,
          address: this.Restaurant.address,
          contact: this.Restaurant.contact,
        }
      );
      if (result.status == 200) {
        this.$router.push({
          name: "Home",
        });
      }
    },
  },
};
</script>
