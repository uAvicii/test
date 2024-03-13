<script>
import mapmost from '@mapmost/mapmost-webgl'
export default {
  name: 'mapmost',
  created() {
    let map = new mapmost.Map({
      container: 'map', // 地图容器 id
      style: 'https://delivery.mapmost.com/cdn/styles/sample_data.json', // 详见 https://www.mapmost.com/mapmost_docs/webgl/latest/docs/map-style
      center: [120.71923008473078, 31.29446443371741], // 起始坐标
      bearing: 50.399999999999636, //方位
      pitch: 78.99999999999993, //倾斜角
      zoom: 14, // 起始缩放等级
      userId: '4836dcb4eb1085b8e865eaf326c2141093d968cd689ed3ded72768acf5c3cfe1'
    })
  }
}
</script>

<template>
  <div id="map" style="width: 100vw; height: 100vh"></div>
</template>
