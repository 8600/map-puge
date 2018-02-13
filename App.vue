<template>
  <div class="map" :style="{width: width +'px', height: height + 'px'}"></div>
</template>

<script>
import L from 'leaflet'
import 'leaflet/dist/leaflet.css'
import 'proj4leaflet'

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
    center: Array,
    zoom: Number
  },
  mounted () {
    const dom = this.$el
    // 需要引入 proj4.js 和 proj4leaflet.js
    L.CRS.Baidu = new L.Proj.CRS('EPSG:900913', '+proj=merc +a=6378206 +b=6356584.314245179 +lat_ts=0.0 +lon_0=0.0 +x_0=0 +y_0=0 +k=1.0 +units=m +nadgrids=@null +wktext  +no_defs', {
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
    L.tileLayer.baidu = function (option) {
      option = option || {}
      let layer
      let subdomains = '0123456789'
      switch (option.layer) {
        // 单图层
        case 'vec': {
          layer = L.tileLayer('http://online{s}.map.bdimg.com/onlinelabel/?qt=tile&x={x}&y={y}&z={z}&styles=' + (option.bigfont ? 'ph' : 'pl') + '&scaler=1&p=1', {
            name: option.name,
            subdomains: subdomains,
            tms: true
          })
          break
        }
      }
      return layer
    }
    const map = L.map(dom, {
      crs: L.CRS.Baidu,
      minZoom: 3,
      maxZoom: 18,
      attributionControl: false
    }).setView(this.center, this.zoom)
    L.tileLayer.baidu({ layer: 'vec' }).addTo(map)
  }
}
</script>
