<script setup>
import { nextTick, onMounted, ref } from 'vue'
// import typedJS from '../components/typedJs.vue'
const sixResult = ref('')
const showVideo = ref(false)
const showIframe = ref(false)
const iid = ref(null)
// const showOld = ref(false)
const videoSrc = ref('')
const amResult = ref('')
// const amOldResult = ref('')
const phText = ref('晚上好, 妈妈')
const isDisabled = ref(true)
const showIframeFn = () => {
  showIframe.value = !showIframe.value
  
  nextTick(()=>{
    document.documentElement.scrollTop = 450
  })
}
const liveVideo = ()=>{
  // videoSrc.value = `https://macaujc.com/static/video/${amResult.value.issue}.mp4`
  videoSrc.value = `https://tv49.macaumarksix.live/lottery/video/2023/2032/${amResult.value.issue}.mp4`
  showVideo.value = !showVideo.value
}
// https://kaijiangapi.net/api/trial/drawResult?code=hk6&format=json&rows=1
// https://tv49.macaumarksix.live/lottery/video/2023/2032/2023120.mp4
const fetchData = async () => {
  fetch('https://1680660.com/smallSix/findSmallSixInfo.do', {
    method: 'GET',
    // headers: {
    //   // ':authority': '1680660.com',
    //   // referer: 'https://6hch.com/'
    // },
    // // referrer: 'https://6hch.com/',
    // mode: 'cors',
    // cache: 'no-cache'
  })
    .then((res) => {
      return res.json()
    })
    .then((res) => {
      console.log(res)
      let a = res.result.data
      if (
        typeof a.preDrawCode == 'string' &&
        typeof a.preDrawIssue == 'number' &&
        typeof a.preDrawTime == 'string'
      ) {
        sixResult.value = res.result.data
      }
    })

  // let res = await fetch(`https://api.bjjfnet.com/data/opencode/2032`, {
  //   method: 'GET'
  // })
  // const json = await res.json()
  // console.log(json)
  // let flag = true
  // for (let key in json.data[0]) {
  //   if (typeof json.data[0][key] !== 'string') {
  //     flag = false
  //   }
  // }
  // if (flag) {
  //   amResult.value = json.data[0]
  // }

  // fetch('https://bet.hkjc.com/contentserver/jcbw/cmc/last30draw.json', 
  // {
  //   method: 'GET',
  //   mode: 'no-cors',
  //   headers: {
  //     'Referer': 'none',
  //     'Sec-Fetch-Dest':'document',
  //     'Sec-Fetch-Mode':'no-navigate',
  //     'Sec-Fetch-Site':'none',
  //     'Sec-Fetch-User':'?1',
  //     'Upgrade-Insecure-Requests':'1',
  // }
  // })
  //   .then((res) => {
  //     // eslint-disable-next-line no-debugger
  //     debugger;
  //     // let a = res.json()
  //     // console.log(a)

  //     return res
  //   })
  //   .catch(err=>console.log(err))
  //   .then((res) => {
  //     // eslint-disable-next-line no-debugger
  //     debugger;
  //     console.log(res)
  //     let a = res[0]
  //     if (
  //       typeof a.id == 'string' &&
  //       typeof a.no == 'string' &&
  //       typeof a.sno == 'string' &&
  //       typeof a.date == 'string'
  //     ) {
  //       sixResult.value = res[0]
  //     }
  //   })
  //   .catch(err=>console.log(err))
  



    fetch('https://api.macaujc.org/api/opencode/2032')
    .then((res) => {
      return res.json()
    })
    .then((res) => {
      console.log(res)
      let a = res.data
      if (
        typeof a.issue == 'string' &&
        typeof a.openCode == 'string' &&
        typeof a.openTime == 'string'
      ) {
        amResult.value = a
      }
    })
  // fetch('https://www.macaumarksix.com/api/macaujc2.com')
  //   .then((res) => {
  //     return res.json()
  //   })
  //   .then((res) => {
  //     console.log(res)
  //     let a = res[0]
  //     if (
  //       typeof a.expect == 'string' &&
  //       typeof a.openCode == 'string' &&
  //       typeof a.openTime == 'string' &&
  //       typeof a.wave == 'string' &&
  //       typeof a.zodiac == 'string'
  //     ) {
  //       amResult.value = a
  //     }
  //   })
  // fetch('https://www.macaumarksix.com/api/macaujc.com')
  //   .then((res) => {
  //     return res.json()
  //   })
  //   .then((res) => {
  //     console.log(res)
  //     let a = res[0]
  //     if (
  //       typeof a.expect == 'string' &&
  //       typeof a.openCode == 'string' &&
  //       typeof a.openTime == 'string' &&
  //       typeof a.wave == 'string' &&
  //       typeof a.zodiac == 'string'
  //     ) {
  //       amOldResult.value = a
  //     }
  //   })
}

onMounted(async () => {
  fetchData()
})
let count = 0
let timer = null
const openInput = () => {
  clearTimeout(timer)
  count++
  if (count === 3) {
    isDisabled.value = false
    return
  }
  timer = setTimeout(() => {
    count = 0
  }, 500)
}

const goToSearch = (e) => {
  window.open(`https://cn.bing.com/search?q=${e.target.value}`, '_blank')
}
</script>

<template>
      <iframe height="1035px" v-if="showIframe" id="iid" :ref="iid" width="100%" sandbox src="https://bet.hkjc.com/marksix/index.aspx?lang=ch"></iframe>
  
  <div class="bg">
    <div class="circleAnimate"></div>
    <div id="element"></div>
    <!-- <typedJS></typedJS> -->
    <div class="search" @click="openInput">
      <input :disabled="isDisabled" :placeholder="phText" @keyup.enter="goToSearch($event)" />
    </div>
    <div style="padding-top: 35vh; font-size: 20px; color: red">
      <div
        class="freshBtn"
        @click="
          () => {
            phText = '刷新没用就找儿子'
            fetchData()
          }
        "
        style="
          margin: 0 auto;
          line-height: 2;
          border-radius: 2rem;
          width: 50vw;
          text-align: center;
          background: mediumturquoise;
          color: #111;
        "
      >
        刷新一下
      </div>
      <p>{{ sixResult.preDrawTime}}</p>
      <span>{{ sixResult.preDrawIssue }} -- 香港</span>
      <button @click="showIframeFn">官网</button>
      <div style="background: darkslateblue; padding: 12px; font-size: 30px">
        <span
          class="ball"
          :style="index == 6 ? 'margin-left: 15px;color:blue' : ''"
          v-for="(item, index) in sixResult.preDrawCode?.split(',')"
          :key="index"
        >
          {{ item }}
        </span>
      </div>
    </div>
    <hr />
    <div style="font-size: 20px; color: red">
      <p>{{ amResult.openTime }}</p>
      <span>{{ amResult.issue }} -- 新澳门</span>
      <button @click="liveVideo">直播回放视频</button>
      <div style="background: darkslateblue; padding: 12px; font-size: 30px">
        <span
          class="ball"
          :style="index == 6 ? 'margin-left: 15px;color:blue' : ''"
          v-for="(item, index) in amResult.openCode?.split(',')"
          :key="index"
        >
          {{ item }}
        </span>
      </div>
      <video v-if="showVideo" controls style="width: 100vw;" :src="videoSrc"></video>
    </div>
    <!-- <button @click="showOld=!showOld">{{!showOld?'点击查看旧澳门':'收起'}}</button>
    <div v-if="showOld" style="font-size: 20px; color: red">
      <p>{{ amOldResult.openTime }}</p>
      <span>{{ amOldResult.expect }} -- 旧澳门</span>
      <div style="background: darkslateblue; padding: 12px; font-size: 30px">
        <span
          class="ball"
          style="color: #fff;"
          :style="{background: `${amOldResult.wave?.split(',')[index]}`, marginLeft: `${index==6?'15px':''}`}"
          v-for="(item, index) in amOldResult.openCode?.split(',')"
          :key="index"
        >
          {{ item }}
        </span>
      </div>
    </div> -->
  </div>
</template>

<style lang="scss" scoped>
.freshBtn {
  transition: all 0.5s;
}
.freshBtn:active {
  color: #fff !important;
  background: rgb(130, 204, 201) !important;
  transform: scale(1.2);
}

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
