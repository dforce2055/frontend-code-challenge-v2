<script setup>
import Blog from "./components/Blog"
const title = "Blog";
</script>
<template>
  <div>
    <h8k-navbar v-bind:header="title"></h8k-navbar>
    <Blog/>
  </div>
</template>
<style lang="scss">
@import '../node_modules/h8k-design/dist/index.css';
</style>