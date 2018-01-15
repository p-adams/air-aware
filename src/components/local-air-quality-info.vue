<template>
  <div>
      Air quality near you
  </div>
</template>
<script>
const KEY = "LRNaGJDPJvJEkdWuP";
export default {
  name: "LocalAirQualityInfo",
  created() {
    this.$http
      .get(
        `http://api.airvisual.com/v2/city?city=Los Angeles&state=California&country=USA&key=${KEY}`
      )
      .then(results => console.log(results));
  }
};
</script>
