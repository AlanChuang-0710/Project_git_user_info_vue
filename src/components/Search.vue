<template lang="">
  <section class="jumbotron">
    <h3 class="jumbotron-heading">Search Github Users</h3>
    <div>
      <input type="text" placeholder="enter the name you search" v-model="keyWord" @keyup.enter="searchUser" />&nbsp;
      <button @click="searchUser">Search</button>
    </div>
  </section>
</template>

<script>
import axios from "axios";

export default {
  name: "Search",
  data() {
    return {
      keyWord: "",
    };
  },
  methods: {
    searchUser() {
      this.$bus.$emit("demoUser", { isFirst: false, isLoading: true, isError: false, userList: [] });

      axios.get(`https://api.github.com/search/users?q=${this.keyWord}`).then(
        (response) => {
          this.$bus.$emit("demoUser", {
            isLoading: false,
            userList: response.data.items,
          });
        },
        (error) => {
          console.log(error);
          this.$bus.$emit("demoUser", {
            isLoading: false,
            isError: error.message,
            userList: [],
          });
        }
      );
    },
  },
};
</script>

<style lang="css" scoped></style>
