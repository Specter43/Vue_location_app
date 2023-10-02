<template>
  <div v-if="location">
    <h3>Time Zone and Local Time</h3>
    <p><strong>Location:</strong> {{ name }}</p>
    <p><strong>Time Zone:</strong> {{ timeZone }}</p>
    <p><strong>Local Time:</strong> {{ localTime }}</p>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  props: {
    location: Object
  },
  data() {
    return {
      timeZone: '',
      localTime: ''
    };
  },
  watch: {
    location: {
      immediate: true,
      handler(newVal) {
        if (newVal) {
          this.fetchTimeZone(newVal.lat, newVal.lng);
        }
      }
    }
  },
  methods: {
    async fetchTimeZone(lat, lng) {
      try {
        const API_KEY = '4TDWFCMBY51J'; // Replace with your TimezoneDb API key

        const response = await axios.get(`http://api.timezonedb.com/v2.1/get-time-zone`, {
          params: {
            key: API_KEY,
            format: 'json',
            by: 'position',
            lat: lat,
            lng: lng
          }
        });


        this.timeZone = response.data.zoneName;
        this.localTime = response.data.formatted;
      } catch (error) {
        console.error('Error fetching time zone data:', error);
      }
    }
  }
}
</script>

<style>
/* Optional styles for the component */
</style>
