<template>
    <q-card>
        <q-card-title>Your local air quality</q-card-title>
        <q-card-main>
            <q-list>
                <q-list-header>Air quality in {{ locationData.city }}</q-list-header>
                <q-item>City: {{ locationData.city }}</q-item>
                <q-item>State: {{ locationData.state }}</q-item>
                <q-item>Country: {{ locationData.country }}</q-item>
                <q-item>Coordinates: {{ coordinates }}</q-item>
                <q-item>
                    <q-list>
                        <q-list-header>Weather</q-list-header>
                        <q-item>Time: {{ weather.ts }}</q-item>
                        <q-item>Humidity: {{ weather.hu }}%</q-item>
                        <q-item>Icon {{ weather.ic }} </q-item>
                        <q-item>Atmospheric pressure: {{ weather.pr }} hPa</q-item>
                        <q-item>Temperature: {{ weather.tp }}</q-item>
                        <q-item>Wind direction: {{ weather.wd }}</q-item>
                        <q-item>Wind speed: {{ weather.ws }}</q-item>
                    </q-list>
                </q-item>
                <q-item>
                    <q-list>
                        <q-list-header>Pollution</q-list-header>
                        <q-item>AQI: {{ pollution.aqius }}</q-item>
                        <q-item>Main pollutant: {{ pollution.mainus }}</q-item>
                    </q-list>
                </q-item>
            </q-list>
        </q-card-main>
    </q-card>
</template>
<script>
import {
  QCard,
  QCardTitle,
  QCardMain,
  QList,
  QListHeader,
  QItem
} from "quasar";
export default {
  name: "FeaturedLocationCard",
  components: {
    QCard,
    QCardTitle,
    QCardMain,
    QList,
    QListHeader,
    QItem
  },
  props: {
    locationData: {
      type: Object,
      required: true,
      default: ""
    }
  },
  computed: {
    coordinates() {
      const location = this.locationData.location.coordinates;
      return `longitude: ${location[0]}, latitude: ${location[1]}`;
    },
    weather() {
      return this.locationData.current.weather;
    },
    pollution() {
      return this.locationData.current.pollution;
    }
  }
};
</script>
