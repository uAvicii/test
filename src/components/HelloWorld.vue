<template>
  <div>
    <div><input v-model="text" type="text" @keyup="handleText" /></div>
    <button>{{ btnText || 'loading...' }}</button>
    <p><input v-model="number" type="number" @keyup="handleNum" /></p>
    <button>{{ textBtn || '...' }}</button>
    <p>
      <input type="text" /> <button @click="handleSubmit" :disabled="isShow">{{ btn }}</button>
    </p>
    <hr />
    <hr />
    <hr />
    <p>
      <button @click="handleClick" :disabled="isClick">{{ ntb }}</button> <input type="text" />
    </p>
    <div>
      hello world i am {{ obj.name }} {{ obj.age }} years old <b>{{ num }}</b>
      <button @click="num++">+</button>
    </div>
    <div class="contain">
      <div
        v-for="(item, index) in imgArrs"
        :key="index"
        class="img"
        :style="{ width: imgWidth + 'px', height: imgWidth * (item.height / item.width) + 'px' }"
      >
        <img class="img-item" :src="item.src" :alt="item.name" :title="item.name" />
      </div>
    </div>
  </div>
</template>

<script>
import { debounce, throttle } from '../utils/index.js'
let timer
export default {
  name: '',
  data() {
    return {
      text: '',
      btnText: '',
      textBtn: '',
      number: null,
      btn: 'submit',
      ntb: 'click',
      num: 555,
      imgWidth: 360,
      obj: {
        name: 'zhangsan',
        age: 18
      },
      isShow: false,
      isClick: false
    }
  },
  inject: ['imgArrs'],
  created() {
    this.getImgHeight()
  },
  mounted() {},
  methods: {
    // 防抖-封装
    debouncedFunction: debounce(function () {
      this.textBtn = this.number
    }, 1000),
    handleNum() {
      this.debouncedFunction()
    },

    // 防抖-原生
    handleText() {
      clearTimeout(timer)
      timer = setTimeout(() => {
        this.btnText = this.text
      }, 1000)
    },

    // 节流-原生
    handleSubmit() {
      if (this.btn === 'submit' && !this.isShow) {
        this.btn = 'loading...'
        this.isShow = true
        setTimeout(() => {
          this.btn = 'submit'
          this.isShow = false
        }, 3000)
      }
    },

    // 节流-封装
    throttleFunction: throttle(function () {
      this.ntb = 'click'
      this.isClick = false
      console.log('clicked') // 三秒内只会打印一次
    }, 3000),

    handleClick() {
      this.ntb = 'loading...'
      this.isClick = true
      this.throttleFunction()
    },

    // 获取imgArrs中的每一张图片的高度
    getImgHeight() {
      this.imgArrs.forEach((item) => {
        const img = new Image()
        img.src = item.src
        img.onload = () => {
          item.height = img.height
          item.width = img.width
        }
      })
    }
  }
}
</script>

<style scoped lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.contain {
  width: 99vw;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  padding: 20px;
  .img {
    overflow: hidden;
    border-radius: 10px;
    margin-top: 10px;
    .img-item {
      width: 100%;
      display: flex;
      align-items: flex-end;
      justify-content: center;
    }
  }
}
</style>
