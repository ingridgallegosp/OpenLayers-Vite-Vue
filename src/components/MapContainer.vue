<template>
  <div ref="map-root"
       style="width: 100%; height: 100%">
  </div>
</template>

<script>
  import View from 'ol/View'
  import Map from 'ol/Map'
  import TileLayer from 'ol/layer/Tile'
  import OSM from 'ol/source/OSM'

  // importing the OpenLayers stylesheet is required for having
  // good looking buttons!
  import 'ol/ol.css'

  export default {
    name: 'MapContainer',
    components: {},
    props: {},
    mounted() {
      // this is where we create the OpenLayers map
      new Map({
        // the map will be created using the 'map-root' ref
        target: this.$refs['map-root'],
        layers: [
          // adding a background tiled layer
          new TileLayer({
            source: new OSM() // tiles are served by OpenStreetMap
          }),
        ],

        // the map view will initially show the whole world
        view: new View({
          zoom: 0,
          center: [0, 0],
          constrainResolution: true
        }),
      })
    },
  }
</script>

<!-- <template>
  	<div ref="map-root"
       style="width: 100%; height: 100%">
  	</div>
</template>

<script setup>
import Feature from 'ol/Feature.js';
import Map from 'ol/Map.js';
import Point from 'ol/geom/Point.js';
import VectorSource from 'ol/source/Vector.js';
import View from 'ol/View.js';
import { Icon, Style } from 'ol/style.js';
import { Tile as TileLayer, Vector as VectorLayer } from 'ol/layer.js';
import { fromLonLat, toLonLat } from 'ol/proj.js';
import OSM from 'ol/source/OSM';
import XYZ from 'ol/source/XYZ';
import Overlay from 'ol/Overlay.js';
//import TileJSON from 'ol/source/TileJSON';
import { toStringHDMS } from 'ol/coordinate.js';
import { onMounted } from 'vue';

// importing the OpenLayers stylesheet is required for having
// good looking buttons!
//import 'ol/ol.css'

const marcador = new Feature({
  	geometry: new Point(fromLonLat([-78.4866264, -0.1535451])), // En dónde se va a ubicar
});

const marcador3 = new Feature({
	geometry: new Point(fromLonLat([116.390903, 39.904835])), // En dónde se va a ubicar
	style: new Style({
    	image: new Icon({
			src: "../assets/location.png",
			scale: 0.8,
		}),
  }),
});

// Agregamos el marcador al arreglo-debe ser arreglo
const vectorSource = new VectorSource({
  	features: [marcador, marcador3], // A la capa le ponemos los marcadores
});

// Layer marcadores
const vectorLayer = new VectorLayer({
  	source: vectorSource,
});

// Layer mapa
const rasterLayer = new TileLayer({
	source: new OSM(), // idioma oficial de cada pais
	/* source: new XYZ({
		//title: "XYZ map",
		//visible: true,
		url: "http://mt0.google.com/vt/lyrs=m&hl=en&x={x}&y={y}&z={z}",
  	}),  */
});

//Crear mapa
const map = new Map({
	layers: [rasterLayer, vectorLayer],
	target: document.getElementById('map'),
	view: new View({
		//center: fromLonLat([0,0]),
		center: fromLonLat([116.390903, 39.904835]),
		//zoom:3,
		zoom: 12,
		//se Manipula lo min y max a mostrar
		//minZoom:2,
		//maxZoom:12
  	}),
});

onMounted(() => {
	map
    //console.log('Componente cargado')
})
</script> -->