# Map
---
使用 example
// initialize the map on the "map" div with a given center and zoom
```
var map = L.map('map', {
	center: [51.505, -0.09],
	zoom: 13
});
```

---

### 构造器

|构造器 | 描述 |
|-------|-------|
|L.map(<String> id, <Map options> options?) | 通过元素ID实例化地图|
|L.map(<HTMLElement> el, <Map options> options?) | 通过HTML元素实例化地图|
---

### 选项

|选项 | 类型 | 默认值 | 描述 |
|-------|-------|-------|-------|
|preferCanvas | Boolean| false| 是否使用Canvas渲染路径|

---

### 控制选项

|选项 | 类型 | 默认值 | 描述 |
|-------|-------|-------|-------|
|zoomControl|	Boolean	|true	|确定zoom control是否默认加载在地图上 .|
|attributionControl	|Boolean	|true	|确定attribution control是否默认加载在地图上.|
---

### 交互设置

|选项 | 类型 | 默认值 | 描述 |
|-------|-------|-------|-------|
|closePopupOnClick|	Boolean	true|	当你不想用户点击地图关闭消息弹出框时，请将其设置为false .|
|zoomSnap|	Number|	1 强制地图的缩放级别始终是其倍数|
|zoomDelta|	Number|	1 按下键盘上的+或 - 或使用缩放控件后，控制地图的缩放级别将改变多少。|
|trackResize|	Boolean	true|	确定地图在窗口尺寸改变时是否可以自动处理浏览器以更新视图.|
|boxZoom|	Boolean	true|	决定地图是否可被缩放到鼠标拖拽出的矩形的视图，鼠标拖拽时需要同时按住shift键.|
|doubleClickZoom|	Boolean	true|	决定地图是否可被双击缩放.|
|dragging	Boolean|	true|	决定地图是否可被鼠标或触摸拖动.|
---

### 地图状态选项
|选项 | 类型 | 默认值 | 描述 |
|-------|-------|-------|-------|
|crs|	CRS|	L.CRS.EPSG3857|	使用的坐标系|
|center|	LatLng|	null|初始化地图的地理中心.|
|zoom	|Number|	null|	初始化地图的缩放.|
|minZoom|	Number|	null|	地图的最小视图。可以重写地图图层的minZoom.|
|maxZoom|	Number|	null|	地图的最大视图。可以重写地图图层的maxZoom.|
|layers|	ILayer[]|	null|	初始化后加载到地图上的图层.|

|maxBounds|	LatLngBounds|	null|	当这个选项被设置后，地图被限制在给定的地理边界内，当用户平移将地图拖动到视图以外的范围时会出现弹回的效果， 并且也不允许缩小视图到给定范围以外的区域（这取决于地图的尺寸）。 使用setMaxBounds方法可以动态地设置这种约束.|

|renderer|	Renderer|	*| 在地图上绘制矢量图层的默认方法 SVG/Canvas|