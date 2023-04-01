<script setup>
import { onMounted, ref } from 'vue'
// import typedJS from '../components/typedJs.vue'
const sixResult = ref('')
onMounted(() => {
  fetch('https://1680660.com/smallSix/findSmallSixInfo.do', {
    method: 'GET',
    headers: {
      // ':authority': '1680660.com',
      // referer: 'https://6hch.com/'
    },
    referrer: 'https://6hch.com/',
    mode: 'cors',
    cache: 'no-cache'
  })
    .then((res) => {
      return res.json()
    })
    .then((res) => {
      sixResult.value = res.result.data
    })
})

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
      <input placeholder="晚上好, 妈妈" @keyup.enter="goToSearch($event)" />
    </div>
    <div style="padding-top: 50vh; font-size: 20px; color: red">
      <p>{{ sixResult.preDrawTime }}</p>
      <p>{{ sixResult.preDrawIssue }}</p>
      <p style="background: darkslateblue; padding: 12px; font-size: 30px">
        <span
          class="ball"
          :style="index == 6 ? 'margin-left: 15px;color:blue' : ''"
          v-for="(item, index) in sixResult.preDrawCode?.split(',')"
          :key="index"
        >
          {{ item }}
        </span>
      </p>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.ball {
  width: 45px;
  height: 45px;
  display: inline-flex;
  justify-content: center;
  align-items: center;
  border-radius: 100%;
  background: linear-gradient(135deg, #fff, lightblue);
}
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
