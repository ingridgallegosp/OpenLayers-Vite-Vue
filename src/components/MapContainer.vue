<template>
    <!-- uso de template ref / document.getElementById-->
    <div ref='mapRoot' 
        style="width: 100%; height: 100%">
    </div>
    <br/>
    <div>
        <input type='text' placeholder='ingresa coordenada e.g. 116.3970977, 39.9207883'/>
        <button>Mostrar en Mapa</button>
    </div>
  
</template>

<script setup>
import { onMounted, ref } from 'vue';

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

// Contenedor donde se va a imprimir
const mapRoot = ref(null);

// -2 referencia inicial para grupo de marcadores
const referenciaMarcadores = ref([
    { name: 'China Life Tower', coordenadas: [116.3970977, 39.9207883] },
    { name: 'Zhengyangmen', coordenadas: [116.3827144, 39.9041912] },
    { name: 'Ciudad Prohibida', coordenadas: [116.3827144, 39.9041912] },
    { name: 'Templo del Cielo', coordenadas: [116.3960498, 39.887287] },
]);
console.log(referenciaMarcadores.value[0].name)
const arrayP = referenciaMarcadores
console.log(arrayP.value)

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

// -2
const arrayMarcadores = () => arrayP.value.map((element, i) => {
    element => {
        // -2  grupo de marcadores
        const crearMarcador = new Feature({
            geometry: new Point(fromLonLat(element.value[i].coordenadas)),// En dónde se va a ubicar
            name: element.value[i].name,
            //additionalInfo: element.value[i].additionalInfo,
        });
        //console.log(crearMarcador)

        return crearMarcador
    }
});
console.log(arrayMarcadores());
//crearMarcadores.setStyle(iconStyle); 


const vectorSourceMarcadores = new VectorSource({
  features: arrayMarcadores, // A la capa le ponemos los marcadores
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
            zoom: 12, //menos zoom se aleja, mas zoom se acerca
        }),
    })
})
</script>

