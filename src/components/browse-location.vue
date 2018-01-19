<template>
  <div>
      <q-field
        helper="Add city name then press enter"
        :count="20"
      >
        <q-input
            v-model="city"
            @keydown.enter="captureCityFromInput"
        />
      </q-field>
  </div>
</template>
<script>
import { QField, QInput } from "quasar";
export default {
  name: "BrowseLocation",
  components: {
    QField,
    QInput
  },
  created() {
    this.findCoordinates();
  },
  data() {
    return {
      city: ""
    };
  },
  methods: {
    captureCityFromInput() {
      const city = this.city.trim();
    },
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
