<script setup>
import { onMounted, ref } from "vue";
import mapboxgl from "mapbox-gl";
import "mapbox-gl/dist/mapbox-gl.css";
import style from "./mapbox/style.json";

mapboxgl.accessToken = "pk.eyJ1IjoiY3ByZW5kZXJnYXN0IiwiYSI6ImNtMjZhYjBicjA3czQyam9rMm83N3l5cmYifQ.vL3eE67Ua2dk5belzAYurQ";

const mapContainer = ref();

onMounted(() => {
  const map = new mapboxgl.Map({
    "container": mapContainer.value,
    "style": style
  });

   // Add zoom and rotation controls to the map.
   map.addControl(new mapboxgl.NavigationControl());
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