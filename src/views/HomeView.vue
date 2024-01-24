<template>
  <div class="container" ref="container">
    <div class="col" v-for="(col, index) in columns" :key="index">
      <div
        ref="pic"
        class="pic"
        v-for="item in col.picList"
        :key="item.name"
        :style="{ width: `${imgItemWidth}px`, height: `${item._height}px` }"
      >
        <img :src="item.src" style="width: 100%" />
        <div class="pic-mask" :style="{ height: `${item._height}px` }">
          <div class="pic-name">{{ item.name }}</div>
        </div>
      </div>
    </div>
  </div>
</template>
  <script>
export default {
  name: 'waterfall',
  data() {
    const imgArr = [
      'https://film-grab.com/wp-content/uploads/2022/07/The-Adjuster-006.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Live-and-Let-Die-061.jpg',
      'https://film-grab.com/wp-content/uploads/2022/07/After-Yang026.jpg',
      'https://film-grab.com/wp-content/uploads/2022/07/The-Worst-Person-in-the-World-001.jpg',
      'https://film-grab.com/wp-content/uploads/2020/10/Zeroville-025.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Bigger-Than-Life-029.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Diamonds-are-Forever-060.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Prisoners-of-Ghostland-002.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Dune-2021-022.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Celeste-005.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/On-Her-Majestys-Secret-Service-023.jpg',
      'https://film-grab.com/wp-content/uploads/2022/05/NightmareAlley010.jpg',
      'https://film-grab.com/wp-content/uploads/2022/05/Paris-13th010.jpg',
      'https://film-grab.com/wp-content/uploads/2020/10/Taking-Off-019.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/The-Eyes-of-Tammy-Faye-001.jpg',
      'https://film-grab.com/wp-content/uploads/2022/05/CmonCmon019.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Frighteners-021.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/You-Only-Live-Twice-003.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/In-Which-We-Serve-008.jpg',
      'https://film-grab.com/wp-content/uploads/2022/05/Apollo101_2036.jpg',
      'https://film-grab.com/wp-content/uploads/2022/05/InTheEarth035.jpg',
      'https://film-grab.com/wp-content/uploads/2022/05/3Iron042.jpg',
      'https://film-grab.com/wp-content/uploads/2022/05/Femme-Fatale049.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Thunderball-005.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/The-Card-Counter-032.jpg',
      'https://film-grab.com/wp-content/uploads/2022/05/The-Apartment003.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Goldfinger-015.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/His-House-047.jpg',
      'https://film-grab.com/wp-content/uploads/2021/09/Der-Prozess-004.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Dillinger-is-Dead-028.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Domain-007.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/From-Russia-With-Love-002.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Master-Z-052.jpg',
      'https://film-grab.com/wp-content/uploads/2019/10/Friday-the-13th-Part-5-056.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Universal-Soldier-The-Return-003.jpg',
      'https://film-grab.com/wp-content/uploads/2022/05/Intrusion016.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/The-Canterbury-Tales-016.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Universal-Soldier-008.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Ip-Man-4-047.jpg',
      'https://film-grab.com/wp-content/uploads/2021/10/Shadow-Film-01.jpg',
      'https://film-grab.com/wp-content/uploads/2021/10/Les-Chants-de-Maldoror-011.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Desert-Hearts-024.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Straight-Time-005.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Ip-Man-3-006.jpg',
      'https://film-grab.com/wp-content/uploads/2021/09/Emperor-Tomato-Ketchup-020.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Black-Widow-009.jpg',
      'https://film-grab.com/wp-content/uploads/2020/10/Border-006.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Green-Inferno-029.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/The-Damned-013.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Ip-Man-2-054.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Passing-001.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Master-of-the-House-003.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Outside-Satan-003.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Black-Orpheus-043.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Ip-Man-001.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Last-Night-In-Soho-023.jpg',
      'https://film-grab.com/wp-content/uploads/2021/09/Explorers-039.jpg',
      'https://film-grab.com/wp-content/uploads/2021/10/Me-and-Earl-028.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Annette-014.jpg',
      'https://film-grab.com/wp-content/uploads/2021/10/The-Rubber-05.jpg',
      'https://film-grab.com/wp-content/uploads/2021/10/Hana-Bi-046.jpg'
    ].map((el) => {
      return {
        src: el,
        name: el.substring(49)
      }
    })
    return {
      imgArr,
      columns: [],
      loadedCount: 0,
      imgItemWidth: 360, // 图片宽度
      gap: 20, // 间隙
      times: null
    }
  },
  async mounted() {
    await this.picLoad()
    this.initData()
    window.onresize = () => {
      if (this.times) {
        clearTimeout(this.times)
      }
      this.times = setTimeout(() => {
        this.initData()
      }, 500)
    }
  },
  methods: {
    picLoad() {
      return new Promise((resolve) => {
        this.imgArr.forEach((item) => {
          if (!item.src) {
            this.loadedCount++
            item['_height'] = 0
            if (this.loadedCount == this.imgArr.length) {
              resolve()
            }
          } else {
            let img = new Image()
            img.src = item.src
            img.onload = () => {
              this.loadedCount++
              item['_height'] = Math.round(this.imgItemWidth * (img.height / img.width))
              if (this.loadedCount == this.imgArr.length) {
                resolve()
              }
            }
            img.onerror = () => {
              this.loadedCount++
              item['_height'] = 0
              if (this.loadedCount == this.imgArr.length) {
                resolve()
              }
            }
          }
        })
      })
    },
    initData() {
      let clientWidth = this.$refs.container.clientWidth, // 页面视图容器宽度
        cols = Math.floor(clientWidth / (this.imgItemWidth + this.gap)), // 计算显示列数
        columns = []
      // 初始每列首行元素
      for (let i = 0; i < cols; i++) {
        this.imgArr[i]['_top'] = 0
        columns.push({ picList: [this.imgArr[i]] })
      }
      // 处理剩余元素
      for (let i = cols; i < this.imgArr.length; i++) {
        let minHeight = this.getMin(columns)
        this.imgArr[i]['_top'] = minHeight.height
        columns[minHeight.index]['picList'].push(this.imgArr[i])
      }
      this.columns = columns
    },
    getMin(columns) {
      let index = 0,
        min = columns.reduce((prev, cur, i) => {
          let _cur = cur.picList[cur.picList.length - 1],
            h = parseInt(_cur._top) + parseInt(_cur._height)
          if (prev == 0) {
            return h
          } else if (h < prev) {
            index = i
            return h
          } else {
            return prev
          }
        }, 0)
      return { height: min, index }
    }
  }
}
</script>

<style lang="scss" scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.container {
  width: 99vw;
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
  padding: 0 20px 20px;
  .pic {
    overflow: hidden;
    border-radius: 10px;
    margin-top: 20px;
    transition: all 0.6s;
    &-mask {
      width: 100%;
      background-color: rgba(0, 0, 0, 0);
      transition: background-color 4s;
      transform: translateY(-100%);
      display: flex;
      align-items: flex-end;
      justify-content: center;
      .pic-name {
        height: 30px;
        text-align: center;
        font-weight: bold;
        color: transparent;
        transform: translateY(30px);
        transition: all 1s;
      }
    }
    &-mask:hover {
      background-color: rgba(0, 0, 0, 0.4);
      transition: background-color 4s linear 0.5s;
      .pic-name {
        color: #fff;
        transform: translateY(0px);
        transition: all 1s;
      }
    }
  }
  .pic:hover {
    transform: translateY(-10px);
    transition: all 0.6s;
  }
}
</style>
