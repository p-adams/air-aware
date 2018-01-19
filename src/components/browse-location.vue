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
  data() {
    return {
      city: "",
      state: "",
      country: "",
      latitude: "",
      longitude: ""
    };
  },
  methods: {
    captureCityFromInput() {
      const city = this.city;
      this.$http
        .get(
          `https://maps.googleapis.com/maps/api/geocode/json?address=${
            this.city
          }`
        )
        .then(geoCoords => {
          this.state =
            geoCoords.data.results[0].address_components[2].long_name;
          this.country =
            geoCoords.data.results[0].address_components[3].short_name;
          const coordinates = geoCoords.data.results[0].geometry.location;
          this.latitude = coordinates.lat;
          this.longitude = coordinates.lng;
        })
        .catch(errorSearchingForCity => console.error(errorSearchingForCity));
    }
  }
};
</script>
