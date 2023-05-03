<template>
    <!-- uso de template ref -->
    <div ref="mapRoot" 
        style="width: 100%; height: 100%">
    </div>
  
</template>

<script setup>
import 'ol/ol.css' // importing the OpenLayers stylesheet is required for having good looking buttons!
import Map from 'ol/Map.js';
import View from 'ol/View.js';
import Feature from 'ol/Feature.js';
import Point from 'ol/geom/Point.js';
import VectorSource from 'ol/source/Vector.js';
import OSM from 'ol/source/OSM';
import XYZ from 'ol/source/XYZ';
import Overlay from 'ol/Overlay.js';
//import TileJSON from 'ol/source/TileJSON';
import { Icon, Style } from 'ol/style.js';
import { Tile as TileLayer, Vector as VectorLayer } from 'ol/layer.js';
import { fromLonLat, toLonLat } from 'ol/proj.js';
import { toStringHDMS } from 'ol/coordinate.js';

import { onMounted, ref } from 'vue';

const mapRoot = ref(null)

onMounted(() => {
    // this is where we create the OpenLayers map
    new Map({
        // the map will be created using the 'mapRoot' ref
        target: mapRoot.value,
        layers: [
            // adding a background tiled layer
            new TileLayer({
                //source: new OSM() // tiles are served by OpenStreetMap
                source: new XYZ({
                    url: 'http://mt0.google.com/vt/lyrs=m&hl=en&x={x}&y={y}&z={z}'
                })
            }),
        ],

        view: new View({
            center: fromLonLat([116.390903, 39.904835]),
            zoom: 12, 
        }),
    })
})
</script>

