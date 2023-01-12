<template lang="">
  <div class="row">
    <h1 v-show="userObj.isFirst">&nbsp;歡迎來到GitHub用戶搜索網站</h1>
    <h1 v-show="userObj.isLoading">&nbsp;正在加載~</h1>
    <h1 v-show="userObj.isError">&nbsp; 無法加載 {{ userObj.isError }}</h1>

    <div class="card" v-for="user in userObj.userList" :key="user.id">
      <a :href="user.html_url" target="_blank">
        <img :src="user.avatar_url" style="width: 100px" />
      </a>
      <p class="card-text">{{ user.login }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "List",
  data() {
    return {
      userObj: {
        userList: [],
        isFirst: true,
        isLoading: false,
        isError: "",
      },
    };
  },
  mounted() {
    this.$bus.$on("demoUser", (userObj) => {
      // 後面的userObj覆蓋前面相同的屬性
      this.userObj = { ...this.userObj, ...userObj };
    });
  },
};
</script>

<style lang="css" scoped>
h1 {
  padding-left: 20px;
}
</style>
