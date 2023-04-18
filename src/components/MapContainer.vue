<template>
  <div class="mapa" ref="map-root"></div>
</template>

<script>
import Map from "ol/Map.js";
import View from "ol/View.js";
//import OSM from "ol/source/OSM";
import XYZ from "ol/source/XYZ";
import Point from "ol/geom/Point.js";
import Feature from "ol/Feature.js";
import VectorSource from "ol/source/Vector.js";
import { Icon, Style } from "ol/style.js";
import { Tile as TileLayer, Vector as VectorLayer } from "ol/layer.js";
import { fromLonLat } from "ol/proj.js";

//Crear marcadores
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
  //source: new OSM() // idioma oficial de cada pais
  source: new XYZ({
    url: "http://mt0.google.com/vt/lyrs=m&hl=en&x={x}&y={y}&z={z}",
  }),
});
/*
//Crear mapa
const map = new Map({
  layers: [rasterLayer, vectorLayer],
  target: document.getElementById("map"),
  view: new View({
    center: fromLonLat([116.390903, 39.904835]),
    zoom: 12,
  }),
}); */

export default {
  name: "MapContainer",
  components: {},
  props: {},
  mounted() {
    //Se crea  mapa
    new Map({
      // the map will be created using the 'map-root' ref
      target: this.$refs["map-root"],
      layers: [rasterLayer, vectorLayer],
      view: new View({
        center: fromLonLat([116.390903, 39.904835]),
        zoom: 12,
        constrainResolution: true, //?
      }),
    });
  },
};
</script>

<style scoped>
.mapa {
  height: 100%;
  width: 100%;
  display: flex;
}
</style>
