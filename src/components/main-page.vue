<template>
  <div>
    <featured-location-card :location-data="localAirQuality" />
  </div>
</template>
<script>
const KEY = "LRNaGJDPJvJEkdWuP";
import FeaturedLocationCard from "./featured-location-card";
export default {
  name: "MainPage",
  components: {
    FeaturedLocationCard
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
