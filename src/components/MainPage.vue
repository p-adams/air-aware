<template>
  <q-layout>
      <q-toolbar>
          <q-toolbar-title>Air Aware</q-toolbar-title>
          <div slot="subtitle">Monitor harmful air pollution</div>
      </q-toolbar>
     <q-select
        v-model="select"
        :options="supportedCountries"
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
      select: ""
    };
  },
  methods: {
    fetchSupportedCountries() {
      return this.$http
        .get(`http://api.airvisual.com/v2/countries?key=${KEY}`)
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

