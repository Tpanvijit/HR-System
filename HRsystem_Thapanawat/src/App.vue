<script setup>
import MyBar from './views/mybar.vue';
</script>
<template>
  <div id="app">
    <MyBar />
    <router-view />
  </div>
</template>
<script>
export default {
 name :"App",
 components : {
  MyBar },};
</script>
