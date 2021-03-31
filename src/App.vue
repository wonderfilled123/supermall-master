<template>
  <div id="app">
     <!-- router-view 当做是一个容器，它渲染的组件是你使用 vue-router 指定的 -->
    <router-view/>
    <main-tar-bar></main-tar-bar>
  </div>
</template>

<script>
import MainTarBar from 'components/content/maintarbar/MainTarBar.vue'

 
export default {
  name: 'App',
  components: {
    MainTarBar
    
  }
}
</script>

<style>
@import "assets/css/base.css";
</style>
