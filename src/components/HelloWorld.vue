<template>
  <div id="map" class="map"></div>
</template>

<script>
import ol from 'ol/ol.css';
import {Map,View} from 'ol';
import TileLayer from "ol/layer/Tile";
import OSM from "ol/source/OSM";
export default {
  mounted(){
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
      })
    })
  }
}
</script>

<style>
#map{height:100%;}
/*隐藏ol的一些自带元素*/
.ol-attribution,.ol-zoom { display: none;}

</style>