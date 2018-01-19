<template>
    <q-card class="card-outline">
        <q-card-title>Your local air quality</q-card-title>
        <q-card-main>
            <q-list class="list-background">
                <q-list-header>Air quality in {{ locationData.city }}</q-list-header>
                <q-item>City: {{ locationData.city }}</q-item>
                <q-item>State: {{ locationData.state }}</q-item>
                <q-item>Country: {{ locationData.country }}</q-item>
                <q-item>Coordinates: {{ coordinates }}</q-item>
                <q-item>
                    <q-list>
                        <q-list-header>Weather</q-list-header>
                        <q-item>Date/Time: {{ formattedDate }}</q-item>
                        <q-item>Humidity: {{ weather.hu }}%</q-item>
                        <q-item>Atmospheric pressure: {{ weather.pr }} millibars</q-item>
                        <q-item>
                          <span class="select-label">Temperature:</span>
                          <q-select
                            v-model="temperature"
                            :options="selectTempConversion"
                          />
                          <span
                            class="temp-display"
                            v-html="currentTemperature"
                          >{{ currentTemperature }}</span>
                        </q-item>
                        <q-item>Wind direction: {{ weather.wd }}</q-item>
                        <q-item>
                          <span class="select-label">Wind speed:</span>
                          <q-select
                            v-model="speed"
                            :options="selectSpeedConversion"
                          />
                          {{ currentWindSpeed }}
                        </q-item>
                    </q-list>
                </q-item>
                <q-item>
                    <q-list>
                        <q-list-header>Pollution</q-list-header>
                        <q-item>Air quality index [AQI]: {{ pollution.aqius }}</q-item>
                    </q-list>
                </q-item>
            </q-list>
        </q-card-main>
    </q-card>
</template>
<script>
/*
 * Todos:
 *    add more info for atmospheric pressure, wind direction, and wind speed units
 *    provide feedback on AQI levels
 */
import {
  QCard,
  QCardTitle,
  QCardMain,
  QList,
  QListHeader,
  QItem,
  QSelect
} from "quasar";
import dateFormat from "dateformat";
export default {
  name: "FeaturedLocationCard",
  components: {
    QCard,
    QCardTitle,
    QCardMain,
    QList,
    QListHeader,
    QItem,
    QSelect
  },
  props: {
    locationData: {
      type: Object,
      required: true,
      default: ""
    }
  },
  data() {
    return {
      temperature: "F",
      selectTempConversion: [
        { label: "Fahrenheit", value: "F" },
        { label: "Celsius", value: "C" }
      ],
      speed: "mph",
      selectSpeedConversion: [
        { label: "mph", value: "mph" },
        { label: "kph", value: "kph" }
      ]
    };
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
    },
    currentTemperature() {
      const celsiusToFahrenheit = this.weather.tp * 1.8 + 32;
      return this.temperature === "F"
        ? `${celsiusToFahrenheit} &#8457;`
        : `${this.weather.tp} &#8451;`;
    },
    formattedDate() {
      return dateFormat(this.weather.td, "dddd, mmmm dS, yyyy, h:MM:ss TT");
    },
    calculatedMPH() {
      return this.weather.ws * 2.236936;
    },
    currentWindSpeed() {
      let speed =
        this.speed === "mph"
          ? (speed = this.weather.ws * 2.236936)
          : (speed = this.weather.ws * 3.6);
      return `${speed} ${this.speed}`;
    }
  }
};
</script>
<style scoped>
.card-outline {
  background: lightgray;
}
.list-background {
  background: white;
}
.temp-display {
  margin-left: 5px;
}
.select-label {
  margin-right: 5px;
}
</style>
