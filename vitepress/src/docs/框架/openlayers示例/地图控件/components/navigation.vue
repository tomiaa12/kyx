<template>
  <div
    ref="map"
    class="map-example"
  ></div>
</template>

<script lang="ts" setup>
import { onMounted, ref } from "vue"
import "ol/ol.css"
import Map from "ol/Map"
import View from "ol/View"
import TileLayer from "ol/layer/Tile"
import XYZ from "ol/source/XYZ"
import { defaults, ZoomToExtent, Rotate } from "ol/control"

const map = ref()

onMounted(() => {
  new Map({
    view: new View({
      center: [12579156, 3274244], // 坐标
      zoom: 12, // 放大倍数
      rotation: 0.3, // 旋转弧度
    }),

    layers: [
      new TileLayer({
        source: new XYZ({
          url: `http://wprd0{1-4}.is.autonavi.com/appmaptile?x={x}&y={y}&z={z}&lang=zh_cn&size=1&scl=1&style=6`,
          crossOrigin: "anonymous", //跨域
        }),
      }),
      new TileLayer({
        source: new XYZ({
          url: `http://wprd0{1-4}.is.autonavi.com/appmaptile?x={x}&y={y}&z={z}&lang=zh_cn&size=1&scl=1&style=8`,
          crossOrigin: "anonymous", //跨域
        }),
      }),
    ],
    controls: defaults({
      zoomOptions: {
        zoomInTipLabel: "放大",
        zoomOutTipLabel: "缩小",
      },
      rotateOptions: {
        autoHide: false,
        label: "↑",
        tipLabel: "重置旋转0°",
      },
    }).extend([
      new ZoomToExtent({
        tipLabel: "缩放至广州",
        label: "Z",
        extent: [
          // 视口大小四个点坐标
          12583177, 2639953, 12622469, 2669156,
        ],
      }),
      new Rotate(), // 旋转控件
    ]),
    target: map.value,
  })
})
</script>

<style lang="scss" scoped>
.map-example {
  width: 100%;
  height: 80vh;
}
</style>
