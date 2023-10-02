<template>
  <div id="app">
    <LocationSearch v-if="currentLocation" :currentLocation="currentLocation" :locations="locations" :zoom="zoom" />
    
    <MapDisplay :currentLocation="currentLocation" :zoom="zoom" :locations="locations" @locationChanged="updateCurrentLocation" />

    <LocationsTable v-if="currentLocation" :currentLocation="currentLocation" :locations="locations" :zoom="zoom" />
    
    <TimeZoneDisplay :location="currentLocation" />
  </div>
</template>

<script>
import LocationSearch from './components/LocationSearch.vue';
import MapDisplay from './components/MapDisplay.vue';
import LocationsTable from './components/LocationsTable.vue';
import TimeZoneDisplay from './components/TimeZoneDisplay.vue';

export default {
  components: {
    LocationSearch,
    MapDisplay,
    LocationsTable,
    TimeZoneDisplay
  },
  data() {
    return {
      // The current location (either from browser geolocation or latest searched location)
      currentLocation: {
        lat: 51.505, // Default latitude (e.g., London)
        lng: -0.1278   // Default longitude (e.g., London)
      },
      zoom: 3,
      locations: [
        { id: 1, name: 'London', lat: 51.5074, lng: -0.1278 },
        { id: 2, name: 'New York', lat: 40.7128, lng: -74.0060 },
        { id: 3, name: 'Tokyo', lat: 35.6895, lng: 139.6917 },
        { id: 4, name: 'Sydney', lat: -33.8688, lng: 151.2093 },
        { id: 5, name: 'Paris', lat: 48.8566, lng: 2.3522 }
        // You can add more cities if you wish
      ],
      // Additional data properties (if any) can be added here...
    };
  },
  methods: {
    addLocation(location) {
      location.id = this.locationIdCounter++;
      this.locations.push(location);
      this.currentLocation = location;
    },
    deleteLocations(idsToDelete) {
      this.locations = this.locations.filter(location => !idsToDelete.includes(location.id));
    },
    updateCurrentLocation(latlng) {
      this.currentLocation = {
        lat: latlng.lat,
        lng: latlng.lng
        // You can add other properties if needed.
      };
      this.fetchTimeZone(latlng.lat, latlng.lng);  // If you're using the fetchTimeZone method I mentioned earlier
    }
  }
}
</script>

<style>
/* Add global styles here if needed */
</style>
