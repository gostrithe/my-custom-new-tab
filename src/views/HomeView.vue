<script setup>
// import { ref } from 'vue'
// import typedJS from '../components/typedJs.vue'

const goToSearch = (e) => {
  window.open(`https://cn.bing.com/search?q=${e.target.value}`, '_blank')
}
</script>

<template>
  <div class="bg">
    <div class="circleAnimate"></div>
    <div id="element"></div>
    <!-- <typedJS></typedJS> -->
    <div class="search">
      <input @keyup.enter="goToSearch($event)" />
    </div>
  </div>
</template>

<style lang="scss" scoped>
.bg {
  position: relative;
  height: 100vh;
  background: url('/bg.webp') no-repeat;
  background-size: 100% 100%;
  .search {
    position: absolute;
    top: 30%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 300px;
    height: 50px;
    background: whitesmoke;
    border-radius: 17px;
    input {
      font-size: 20px;

      font-style: italic;
      font-weight: bold;
      text-align: center;
      outline: none;
      border: 0;
      background: inherit;
      width: 100%;
      height: 100%;
      padding: 0 15px;
      box-sizing: border-box;
      border-radius: inherit;
      &:focus {
        background: #fff;
        box-shadow: inset 0 0 7px rgba($color: #000000, $alpha: 1);
        caret-color: green;
      }
    }
  }
}
</style>
