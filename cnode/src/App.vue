<template>
  <div id="app">
    <Header></Header>
    <div class="main">
      <router-view name="slidebar"></router-view> <!--slidebar 对应 index.js 中的 slidebar-->
      <router-view name="main"></router-view> <!--main 对应 index.js 中的 main-->
    </div>
  </div>
</template>

<script>
  import Header from './components/Header';
  import PostList from './components/PostList';
export default {
  name: 'App',
  components: {
    Header, PostList
  }
}
</script>

<style>
.main {
  width: 80%;
  margin: 0 auto;
}
</style>
