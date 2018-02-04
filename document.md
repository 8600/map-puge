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

构造器

|构造器 | 描述 |
|-------|-------|-------|-------|-------|
|L.map(<String> id, <Map options> options?) | 通过元素ID实例化地图|
|L.map(<HTMLElement> el, <Map options> options?) | 通过HTML元素实例化地图|