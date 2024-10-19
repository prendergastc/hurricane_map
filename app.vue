<script setup>
import { onMounted, ref } from "vue";
import mapboxgl from "mapbox-gl";
import "mapbox-gl/dist/mapbox-gl.css";
import style from "./mapbox/style.json";
import sites from "./data/sites.json";
import neighborhoods from "./data/neighborhoods-with-count.json";


// Get bounding box for sites and log to console.
// import { bbox } from "@turf/turf";

// const sitesBbox = bbox(sites);
// console.log(sitesBbox);

mapboxgl.accessToken = "pk.eyJ1IjoiY3ByZW5kZXJnYXN0IiwiYSI6ImNtMjZhYjBicjA3czQyam9rMm83N3l5cmYifQ.vL3eE67Ua2dk5belzAYurQ";

const mapContainer = ref();

onMounted(() => {
  const map = new mapboxgl.Map({
    "container": mapContainer.value,
    "style": style,
    "bounds": [
      -118.6,
      33.8,
      -118.1,
      34.3
    ],
    "fitBoundsOptions": {
      "padding": 25,
      "pitch": 45
    }
  });

   // Add zoom and rotation controls to the map.
   map.addControl(new mapboxgl.NavigationControl());
   
   // Add load event listener.
   map.on("load", () => {

    // Add sites data after load.
    const sitesSource = map.getSource("sites");
    sitesSource.setData(sites);

    // Add neighborhoods data after load.
    const neighborhoodsSource = map.getSource("neighborhoods");
    neighborhoodsSource.setData(neighborhoods);
   });


});

</script>

<template>
  <div ref="mapContainer" class="map"></div>
</template>

<style scoped>
.map {
  height: 100%;
}
</style>