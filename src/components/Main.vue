<template>
  <div>
    <h2 v-if="firstView">输入用户名搜索</h2>
    <h2 v-if="loading">LOADING....</h2>
    <h2 v-if="errorMsg">{{errorMsg}}</h2>
    <div class="row">
      <div class="card" v-for="(user,index) in users" :key="index">
        <a href="https://github.com/reactjs" target="_blank">
          <img :src="user.avatar_url" style="width: 100px;">
        </a>
        <p class="card_text">{{user.name}}</p>
      </div>
    </div>
  </div>
</template>

<script>
import PubSub from "pubsub-js";
import axios from "axios";
export default {
  data() {
    return {
      firstView: true,
      loading: false,
      errorMsg: "",
      users: null
    };
  },
  mounted() {

    //订阅事件
    PubSub.subscribe("search", (msg, searchName) => {
      //ajax搜索
      const url = `https://api.github.com/search/users?q=${searchName}`;

      //更新请求中的状态
      this.firstView = false;
      this.loading = true;
      this.users = null;
      this.errorMsg = "";

      //发送ajax请求
      axios
        .get(url)
        .then(response => {
          const result = response.data;
          //console.log(result)
          const users = result.items.map(item => ({
            url: item.html_url,
            avatar_url: item.avatar_url,
            name: item.login
          }));
          //成功，更新状态
          this.firstView = false;
           this.loading = false;
          this.users = users;
        })
        .catch(error => {
          this.loading = false;
          this.errorMsg = "请求失败";
        });
    });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
