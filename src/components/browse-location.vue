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
      {{ locationAirQuality }}
  </div>
</template>
<script>
import { QField, QInput } from "quasar";
const KEY = "LRNaGJDPJvJEkdWuP";
export default {
  name: "BrowseLocation",
  components: {
    QField,
    QInput
  },
  data() {
    return {
      city: "",
      latitude: "",
      longitude: "",
      locationAirQuality: ""
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
          const coordinates = geoCoords.data.results[0].geometry.location;
          this.latitude = coordinates.lat;
          this.longitude = coordinates.lng;
          this.locationAirQuality = this.getLocationAirQuality(
            this.latitude,
            this.longitude
          );
        })
        .catch(errorSearchingForCity => console.error(errorSearchingForCity));
    },
    getLocationAirQuality(latitude, longitude) {
      return this.$http
        .get(
          `http://api.airvisual.com/v2/nearest_city?lat=${latitude}&lon=${longitude}&key=${KEY}`
        )
        .then(results => {
          return results.data.data;
        });
    }
  }
};
</script>
