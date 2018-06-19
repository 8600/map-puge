# leaflet

> leaflet 加载百度瓦片地图图层 以及高德 、天地图等国内常用地图

## 参数

| 参数        | 含义         | 类型  | 是否必须  |
| ----------- |:-------------:| -----:| -----:|
|width| 地图的宽度 | Number | false |
|height| 地图的高度| String | false |
|option| 地图配置| Object | false |
|center| 中心点坐标| Array | true |
|zoom| 缩放比例| Number | true |

## option选项

```
{
  // 瓷砖引用源
  "tileLayer": "baidu",
  // 地图样式
  "layer": "simulation"
}
```