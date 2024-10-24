<script setup>
import { onMounted, ref } from "vue";
import mapboxgl from "mapbox-gl";
import "mapbox-gl/dist/mapbox-gl.css";
import style from "./mapbox/style.json";
import atlantic_data from "./data/atlantic/2023/2023_atlantic_summary.json";
import pacific_data from "./data/pacific/2023/2023_pacific_summary.json";

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
    "fitBoundsOptions": {
      "padding": 25,
      "pitch": 45
    }
  });

   // Add zoom and rotation controls to the map.
   map.addControl(new mapboxgl.NavigationControl());
   
   // Add load event listener.
   map.on("load", () => {

    // Add atlantic track data after load.
    const atlanticSource = map.getSource("atlantic");
    atlanticSource.setData(atlantic_data);

    // Add pacific track data after load.
    const pacificSource = map.getSource("pacific");
    pacificSource.setData(pacific_data);

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