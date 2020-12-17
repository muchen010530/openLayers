<template>
  <div id="map">
        <div  class="map" ref="map"></div>
        <div class="ol-popup" id="popup" ref="popup">
            <a href="#" class="ol-popup-closer" id="popup-closer" ref="closer" @click="close">x</a>
            <div id="popup-content" ref="content"></div>
        </div>
  </div>
</template>

<script>
import ol from 'ol/ol.css';
import {Map,View,Overlay} from 'ol';
import TileLayer from "ol/layer/Tile";
import OSM from "ol/source/OSM";
import TileJSON from 'ol/source/TileJSON';
import {toStringHDMS} from 'ol/coordinate';
import {toLonLat} from 'ol/proj';
export default {
    methods:{
        close(){
            //console.log(this.overlay)
            this.overlay.setPosition(undefined) //若要不显示弹出框则只需设置overlay.setPosition(undefined)
        }
    },
  mounted(){
    const overlay = new Overlay({
        element:this.$refs.popup,
        autoPan:true,   //设置点击边缘时地图会自动平移
        autoPanAnimation:{
            duration:250  //自动平移动画时间250ms
        }
    })
    this.overlay = overlay
    const map = new Map({
      layers:[
        new TileLayer({
          source: new OSM()
        })
      ],
      target:'map',
      view:new View({
        center:[0,0],
        zoom:2
      }),
      overlays:[overlay]
    })
    const content = document.getElementById('popup-content')
    map.on('singleclick',function(e){
        const coordinate = e.coordinate
        const hdms = toStringHDMS(toLonLat(coordinate))
        content.innerHTML = "<p>你点击了:</p>" + hdms 
        overlay.setPosition(coordinate) //position，在地图所在的坐标系框架下，overlay 放置的位置；
    })
  }
}
</script>

<style>
#map{height:100%;}
/*隐藏ol的一些自带元素*/
.ol-attribution,.ol-zoom { display: none;}

</style>