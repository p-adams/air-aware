<template>
  <div>
    <q-card>
      <q-card-title>Browse all supported countries</q-card-title>
      <q-card-main>
        <q-btn
          color="primary"
          @click="resetMenus"
        >reset menus</q-btn>
      <h5>Select a country</h5>
        <q-select
            float-label="countries"
            v-model="countrySelect"
            :options="supportedCountries"
        />
        <div v-if="supportedStates.length">
          <h5>Select a state/province</h5>
          <q-select
            float-label="states/provinces"
            v-model="stateSelect"
            :options="supportedStates"
            />
        </div>
        <div v-if="supportedCities.length">
          <h5>Select city</h5>
          <q-select
            float-label="cities"
            @change="selectCity"
            v-model="citySelect"
            :options="supportedCities"
          />
        </div>
      </q-card-main>
    </q-card>
    <div v-if="locationDataDidLoad">
      <featured-location-card :location-data="locationAirQuality"/>
    </div>
  </div>
</template>
<script>
import { QCard, QCardTitle, QCardMain, QSelect, QBtn } from "quasar";
import FeaturedLocationCard from "./featured-location-card";
const KEY = "LRNaGJDPJvJEkdWuP";
export default {
  name: "MainPage",
  components: {
    QCard,
    QCardTitle,
    QCardMain,
    QSelect,
    FeaturedLocationCard,
    QBtn
  },
  created() {
    this.loadCountries();
  },
  data() {
    return {
      supportedCountries: [],
      supportedStates: [],
      supportedCities: [],
      countrySelect: "",
      stateSelect: "",
      citySelect: "",
      locationDataDidLoad: false,
      locationAirQuality: ""
    };
  },
  watch: {
    countrySelect: function() {
      this.supportedStates = [];
      this.fetchSupportedStates().then(states =>
        states.map(s =>
          this.supportedStates.push({ label: s.state, value: s.state })
        )
      );
    },
    stateSelect: function() {
      this.supportedCities = [];
      this.fetchSupportedCities().then(cities =>
        cities.map(c =>
          this.supportedCities.push({ label: c.city, value: c.city })
        )
      );
    }
  },
  methods: {
    loadCountries() {
      this.fetchSupportedCountries().then(countries =>
        countries.map(c =>
          this.supportedCountries.push({ label: c.country, value: c.country })
        )
      );
    },
    fetchSupportedCountries() {
      return this.$http
        .get(`http://api.airvisual.com/v2/countries?key=${KEY}`)
        .then(response => response.data.data)
        .catch(error => console.error(error));
    },
    fetchSupportedStates() {
      return this.$http
        .get(
          `http://api.airvisual.com/v2/states?country=${
            this.countrySelect
          }&key=${KEY}`
        )
        .then(response => response.data.data)
        .catch(error => console.error(error));
    },
    fetchSupportedCities() {
      return this.$http
        .get(
          `http://api.airvisual.com/v2/cities?state=${
            this.stateSelect
          }&country=${this.countrySelect}&key=${KEY}`
        )
        .then(response => response.data.data)
        .catch(error => console.error(error));
    },
    resetMenus() {
      this.supportedCountries = [];
      this.supportedStates = [];
      this.supportedCities = [];
      this.loadCountries();
    },
    selectCity() {
      console.log(this.citySelect);
      this.$http
        .get(
          `https://maps.googleapis.com/maps/api/geocode/json?address=${
            this.citySelect
          }`
        )
        .then(geoCoords => {
          const coordinates = geoCoords.data.results[0].geometry.location;
          this.getLocationAirQuality(coordinates.lat, coordinates.lng);
        })
        .catch(errorSearchingForCity => console.error(errorSearchingForCity));
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
