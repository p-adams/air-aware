<template>
  <div>
    <h5>Select a country</h5>
      <q-select
          v-model="countrySelect"
          :options="supportedCountries"
      />
      <div v-if="supportedStates.length">
        <h5>Select a state/province</h5>
        <q-select
            v-model="stateSelect"
            :options="supportedStates"
          />
      </div>
      <div v-if="supportedCities.length">
        <h5>Select city</h5>
        <q-select
          v-model="citySelect"
          :options="supportedCities"
        />
      </div>
  </div>
</template>
<script>
import { QLayout, QSelect } from "quasar";
const KEY = "LRNaGJDPJvJEkdWuP";
export default {
  name: "MainPage",
  created() {
    this.fetchSupportedCountries().then(countries =>
      countries.map(c =>
        this.supportedCountries.push({ label: c.country, value: c.country })
      )
    );
  },
  data() {
    return {
      supportedCountries: [],
      supportedStates: [],
      supportedCities: [],
      countrySelect: "",
      stateSelect: "",
      citySelect: ""
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
    }
  },
  components: {
    QLayout,
    QSelect
  }
};
</script>
