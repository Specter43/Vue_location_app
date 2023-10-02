<template>
  <div class="map-container" >
    <l-map :center="currentLocation" :zoom="zoom" @click="onMapClick">
      <l-tile-layer url="http://{s}.tile.osm.org/{z}/{x}/{y}.png"></l-tile-layer>
      <l-marker v-for="loc in locations" :key="loc.id" :lat-lng="[loc.lat, loc.lng]"></l-marker>
    </l-map>
  </div>
</template>

<script>
import { LMap, LTileLayer, LMarker } from '@vue-leaflet/vue-leaflet';
import 'leaflet/dist/leaflet.css';

export default {
  components: {
    LMap, LTileLayer, LMarker
  },
  props: {
    currentLocation: Object,
    locations: Array,
    zoom: Number  // Ensure this is here
  },
  methods: {
    onMapClick(event) {
      console.log('Map was clicked!', event);
    }
  }
}

</script>

<style>
.map-container {
  height: 400px; 
  width: 100%;
}
</style>

