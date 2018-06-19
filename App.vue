<template>
  <div class="map" :style="{width: width +'px', height: height + 'px'}"></div>
</template>

<script>
import L from 'leaflet'
import 'leaflet/dist/leaflet.css'
import 'proj4leaflet'
let map = null
export default {
  name: 'Map',
  props: {
    width: {
      type: Number,
      default: 1200
    },
    height: {
      type: Number,
      default: 800
    },
    tileLayer: {
      type: String,
      default: 'baidu'
    },
    customid: {
      type: String,
      default: 'midnight'
    },
    layer: {
      type: String,
      default: 'simulation'
    },
    // 大字体
    bigfont: {
      type: Boolean,
      default: false
    },
    center: Array,
    zoom: Number
  },
  mounted () {
    // 获取dom元素
    const dom = this.$el
    const layer = this.layer
    if (this.tileLayer === 'baidu') {
      map = L.map(dom, {
        crs: this.getBaiDuCRS(),
        minZoom: 3,
        maxZoom: 18,
        attributionControl: false
      }).setView(this.center, this.zoom)
      this.getBaiDuLayer({ layer }).addTo(map)
    }
  },
  methods: {
    // 百度瓷砖地址
    getBaiDuLayer (option = {}) {
      let layer, subdomains = '0123456789'
      switch (option.layer) {
        //单图层
        case "simulation":
        default:
          layer = L.tileLayer('http://online{s}.map.bdimg.com/onlinelabel/?qt=tile&x={x}&y={y}&z={z}&styles=' + (option.bigfont ? 'ph' : 'pl') + '&scaler=1&p=1', {
            name:option.name,
            subdomains: subdomains,
            tms: true
          })
          break
        case "img_d": 
          layer = L.tileLayer('http://shangetu{s}.map.bdimg.com/it/u=x={x};y={y};z={z};v=009;type=sate&fm=46', {
            name: option.name,
            subdomains: subdomains,
            tms: true
          })
          break
        case "img_z":
          layer = L.tileLayer('http://online{s}.map.bdimg.com/tile/?qt=tile&x={x}&y={y}&z={z}&styles=' + (option.bigfont ? 'sh' : 'sl') + '&v=020', {
            name: option.name,
            subdomains: subdomains,
            tms: true
          })
          break
        // Custom 各种自定义样式
        case "custom":
          //可选值：dark,midnight,grayscale,hardedge,light,redalert,googlelite,grassgreen,pink,darkgreen,bluish
          layer = L.tileLayer('http://api{s}.map.bdimg.com/customimage/tile?&x={x}&y={y}&z={z}&scale=1&customid=' + this.customid, {
            name: option.name,
            subdomains: "012",
            tms: true
          })
          break

        case "traffic":// 实时路况
          const time = new Date().getTime();
          layer = L.tileLayer('http://its.map.baidu.com:8002/traffic/TrafficTileService?x={x}&y={y}&level={z}&time=' + time + '&label=web2D&v=017', {
            name: option.name,
            subdomains: subdomains,
            tms: true
          })
          break

        //合并
        case "satellite":
          layer = L.layerGroup([
            this.getBaiDuLayer({ name: "底图", layer: 'img_d', bigfont: option.bigfont }),
            this.getBaiDuLayer({ name: "注记", layer: 'img_z', bigfont: option.bigfont })
          ]);
          break
      }
      return layer
    },
    // 获取百度坐标系
    getBaiDuCRS () {
      // 需要引入 proj4.js 和 proj4leaflet.js
      return new L.Proj.CRS('EPSG:900913', '+proj=merc +a=6378206 +b=6356584.314245179 +lat_ts=0.0 +lon_0=0.0 +x_0=0 +y_0=0 +k=1.0 +units=m +nadgrids=@null +wktext  +no_defs', {
        resolutions: function () {
          const level = 19
          let res = []
          res[0] = Math.pow(2, 18)
          for (var i = 1; i < level; i++) {
            res[i] = Math.pow(2, (18 - i))
          }
          return res
        }(),
        origin: [0, 0],
        bounds: L.bounds([20037508.342789244, 0], [0, 20037508.342789244])
      })
    }
  },
  watch: {
    // 待优化 不知道有用没
    layer (layer) {
      this.getBaiDuLayer({ layer }).addTo(map)
    },
    width () {
      // 检查地图容器的大小是否改变并更新地图，如果是这样的话，在动态改变地图大小后调用，如果animate是true的话，对地图进行更新.
      map.invalidateSize(true)
    },
    height () {
      map.invalidateSize(true)
    }
  }
}
</script>
