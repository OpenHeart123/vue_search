<template>
  <div id="container">
    <search/>
    <Main/>
  </div>
</template>

<script>
import Main from "./components/Main.vue";
import Search from "./components/Search.vue";

export default {
  components: {
    Main,
    Search
  }
};
</script>

<style>
.card {
  float: left;
  width: 33.333%;
  padding: 0.75rem;
  margin-bottom: 2rem;
  border: 1px solid #efefef;
  text-align: center;
}
.card > img {
  margin-bottom: 0.75rem;
  border-radius: 100px;
}
.card-text {
  font-size: 85%;
}
</style>
