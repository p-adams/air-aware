<template>
  <div>
    <q-card>
      <q-card-title>Browse air quality by city name</q-card-title>
      <q-card-main>
        <q-field
          helper="Add city name then press enter"
          :count="20"
        >
          <q-input
              v-model="city"
              @keydown.enter="captureCityFromInput"
              placeholder="For example, Brooklyn..."
          />
        </q-field>
      </q-card-main>
    </q-card>
     <div v-if="locationDataDidLoad">
       <feature-location-card :location-data="locationAirQuality"/>
     </div>
  </div>
</template>
<script>
import { QCard, QCardTitle, QCardMain, QField, QInput } from "quasar";
import FeatureLocationCard from "./featured-location-card";
const KEY = "LRNaGJDPJvJEkdWuP";
export default {
  name: "BrowseLocation",
  components: {
    QCard,
    QCardTitle,
    QCardMain,
    QField,
    QInput,
    FeatureLocationCard
  },
  data() {
    return {
      city: "",
      locationAirQuality: "",
      locationDataDidLoad: false
    };
  },
  methods: {
    captureCityFromInput() {
      this.$http
        .get(
          `https://maps.googleapis.com/maps/api/geocode/json?address=${
            this.city
          }`
        )
        .then(geoCoords => {
          const coordinates = geoCoords.data.results[0].geometry.location;
          this.getLocationAirQuality(coordinates.lat, coordinates.lng);
        })
        .catch(errorSearchingForCity => console.error(errorSearchingForCity));
      this.city = "";
    },
    getLocationAirQuality(latitude, longitude) {
      this.$http
        .get(
          `http://api.airvisual.com/v2/nearest_city?lat=${latitude}&lon=${longitude}&key=${KEY}`
        )
        .then(results => {
          this.locationDataDidLoad = true;
          this.locationAirQuality = results.data.data;
        });
    }
  }
};
</script>
