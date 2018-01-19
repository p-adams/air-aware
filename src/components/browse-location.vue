<template>
  <div></div>
</template>
<script>
export default {
  name: "BrowseLocation",
  created() {
    this.findCoordinates();
  },
  data() {
    return {
      city: "Detroit"
    };
  },
  methods: {
    findCoordinates() {
      this.$http
        .get(
          `https://maps.googleapis.com/maps/api/geocode/json?address=${
            this.city
          }`
        )
        .then(geoCoords => {
          const state = geoCoords.data.results[0].address_components[2];
          const country = geoCoords.data.results[0].address_components[3];
          console.log(state, country);
          const coordinates = geoCoords.data.results[0].geometry.location;
          console.log(coordinates.lat, coordinates.lng);
        });
    }
  }
};
</script>
