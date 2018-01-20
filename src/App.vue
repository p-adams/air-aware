<template>
  <div id="q-app">
    <q-layout ref="layout">
      <q-toolbar slot="header">
        <q-toolbar-title>Air Aware</q-toolbar-title>
        <div slot="subtitle">Monitor harmful air pollution</div>
      </q-toolbar>
      <app-navigation/>
      <router-view />
    </q-layout>
  </div>
</template>

<script>
import { QLayout, QToolbar, QToolbarTitle } from "quasar";
import AppNavigation from "./components/app-navigation";
export default {
  name: "App",
  components: {
    QLayout,
    QToolbar,
    QToolbarTitle,
    AppNavigation
  }
};
</script>
<style scoped>

</style>
