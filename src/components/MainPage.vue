<template>
  <q-layout>
      <q-toolbar>
          <q-toolbar-title>Air Aware</q-toolbar-title>
          <div slot="subtitle">Monitor harmful air pollution</div>
      </q-toolbar>
     <q-select
        v-model="countrySelect"
        :options="supportedCountries"
     />
     <q-select
        v-if="supportedStates.length"
        v-model="stateSelect"
        :options="supportedStates"
      />
      <q-select
        v-if="supportedCities.length"
        v-model="citySelect"
        :options="supportedCities"
      />
   
  </q-layout>
</template>
<script>
import { QLayout, QToolbar, QToolbarTitle, QSelect } from "quasar";
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
          `http://api.airvisual.com/v2/states?country=${this
            .countrySelect}&key=${KEY}`
        )
        .then(response => response.data.data)
        .catch(error => console.error(error));
    },
    fetchSupportedCities() {
      return this.$http
        .get(
          `http://api.airvisual.com/v2/cities?state=${this
            .stateSelect}&country=${this.countrySelect}&key=${KEY}`
        )
        .then(response => response.data.data)
        .catch(error => console.error(error));
    }
  },
  components: {
    QLayout,
    QToolbar,
    QToolbarTitle,
    QSelect
  }
};
</script>

