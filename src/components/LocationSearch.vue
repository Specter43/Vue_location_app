<!-- LocationSearch.vue -->
<template>
    <div>
      <input v-model="searchQuery" @keyup.enter="searchLocation" placeholder="Enter location name...">
      <button @click="searchLocation">Search</button>
      <button @click="getCurrentLocation">Get Current Location</button>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        searchQuery: ''
      };
    },
    methods: {
      async searchLocation() {
        const response = await axios.get(`https://nominatim.openstreetmap.org/search?format=json&q=${this.searchQuery}`);
        const location = response.data[0];
        if (location) {
          this.$emit('locationSelected', { lat: parseFloat(location.lat), lng: parseFloat(location.lon), name: location.display_name });
        } else {
          alert('Location not found!');
        }
      },
      getCurrentLocation() {
        if (navigator.geolocation) {
          navigator.geolocation.getCurrentPosition(position => {
            const lat = position.coords.latitude;
            const lng = position.coords.longitude;
            this.$emit('locationSelected', { lat, lng });
          });
        } else {
          alert('Geolocation is not supported by this browser.');
        }
      }
    }
  }
  </script>
  