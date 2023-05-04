<template>
    <!-- uso de template ref / document.getElementById-->
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
//import OSM from 'ol/source/OSM';
//import TileJSON from 'ol/source/TileJSON';
import XYZ from 'ol/source/XYZ';
import Overlay from 'ol/Overlay.js';
import { Icon, Style } from 'ol/style.js';
import { Tile as TileLayer, Vector as VectorLayer } from 'ol/layer.js';
import { fromLonLat, toLonLat } from 'ol/proj.js';
import { toStringHDMS } from 'ol/coordinate.js';
import { onMounted, ref } from 'vue';

// Contenedor donde se va a imprimir
const mapRoot = ref(null)

// Crear marcador
const marcador2 = new Feature({
    geometry: new Point(fromLonLat([116.390903, 39.904835])),// En dónde se va a ubicar
    name: 'Beijing',
    additionalInfo: 'Capital de China',
});

// Estilo para el marcador
const iconStyle = new Style({
    image: new Icon({
        color: '#BADA55',
        crossOrigin: 'anonymous',
        src: "src/assets/location.png",
        scale: 0.1,
    })
  }); 

marcador2.setStyle(iconStyle); 

// Agregamos el marcador al arreglo
const vectorSource = new VectorSource({
  features: [ marcador2], // A la capa le ponemos los marcadores
});

// Layer marcadores
const vectorLayer = new VectorLayer({
  source: vectorSource,
});

// Layer mapa
const rasterLayer = new TileLayer({
    //source: new OSM() // idioma oficial de cada pais-mapa de open street map
    /* source: new TileJSON({
      url: 'https://a.tiles.mapbox.com/v3/aj.1x1-degrees.json?secure=1',
      crossOrigin: '',
    }) */
    source: new XYZ({
      url: 'http://mt0.google.com/vt/lyrs=m&hl=en&x={x}&y={y}&z={z}'//mapa de google
    })
      
});

// Creamos/montamos el mapa
onMounted(() => {
    new Map({
        // el mapa se va a crear usando el template ref 'mapRoot'
        target: mapRoot.value,
        layers: [rasterLayer, vectorLayer],
        view: new View({
            center: fromLonLat([116.390903, 39.904835]),
            zoom: 10, //menos zoom se aleja, mas zoom se acerca
        }),
    })
})
</script>

