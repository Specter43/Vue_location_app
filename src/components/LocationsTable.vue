<template>
  <div>
    <button @click="deleteSelectedLocations">Delete Selected</button>

    <table>
      <thead>
        <tr>
          <th>Select</th>
          <th>Latitude</th>
          <th>Longitude</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="location in locations" :key="location.id">
          <td><input type="checkbox" v-model="selectedLocations[location.id]" /></td>
          <td>{{ location.lat }}</td>
          <td>{{ location.lng }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    locations: Array
  },
  data() {
    return {
      selectedLocations: {}
    };
  },
  methods: {
    deleteSelectedLocations() {
      for (let id in this.selectedLocations) {
        if (this.selectedLocations[id]) {
          this.$emit('delete-location', id);
        }
      }
      this.selectedLocations = {};  // Reset selections
    }
  }
}
</script>
