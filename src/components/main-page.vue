<template>
  <div>
    <q-card>
      <q-card-title>Air quality in {{ cityData }}</q-card-title>
      <q-card-main>
        <p> {{ stateData }} </p>
        <p>{{ localAirQuality }}
        </p>
        </q-card-main>
    </q-card>
  </div>
</template>
<script>
const KEY = "LRNaGJDPJvJEkdWuP";
import { QCard, QCardTitle, QCardMain } from "quasar";
export default {
  name: "MainPage",
  components: {
    QCard,
    QCardTitle,
    QCardMain
  },
  created() {
    this.$http
      .get(
        `http://api.airvisual.com/v2/city?city=Detroit&state=Michigan&country=USA&key=${KEY}`
      )
      .then(results => (this.localAirQuality = results.data.data));
  },
  data() {
    return {
      localAirQuality: ""
    };
  },
  computed: {
    cityData() {
      return this.localAirQuality.city;
    },
    stateData() {
      return this.localAirQuality.state;
    }
  }
};
</script>
