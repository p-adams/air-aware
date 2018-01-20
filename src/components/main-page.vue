<template>
  <div class="container">
    <q-carousel
      class="text-white"
      dots
    >
      <div slot="slide" class="bg-secondary">
        Air Aware is an application that provides reliable, real-time air quality information...
      </div>
      <div slot="slide" class="bg-secondary">
        Browse locations near you...
      </div>
      <div slot="slide" class="bg-secondary">
        Browse air quality information in all supported countries...
      </div>
    </q-carousel>
  </div>
</template>
<script>
import { QCarousel } from "quasar";
export default {
  name: "MainPage",
  components: {
    QCarousel
  }
};
</script>
<style scoped>
.container {
  margin-top: 60px;
}
</style>
