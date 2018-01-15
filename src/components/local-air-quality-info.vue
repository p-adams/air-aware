<template>
  <div>
      <h5>Air quality in {{ cityData }}</h5>
  </div>
</template>
<script>
const KEY = "LRNaGJDPJvJEkdWuP";
export default {
  name: "LocalAirQualityInfo",
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
    }
  }
};
</script>
