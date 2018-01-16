<template>
  <div>
    <featured-location-card
      v-if="dataDidLoad"
      :location-data="localAirQuality"
    />
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
      .then(results => {
        this.dataDidLoad = true;
        this.localAirQuality = results.data.data;
      });
  },
  data() {
    return {
      localAirQuality: "",
      dataDidLoad: false
    };
  }
};
</script>
