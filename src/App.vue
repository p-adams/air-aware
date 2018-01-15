<template>
  <div id="q-app">
    <q-layout ref="layout">
      <q-toolbar slot="header">
        <q-toolbar-title>Air Aware</q-toolbar-title>
        <div slot="subtitle">Monitor harmful air pollution</div>
      </q-toolbar>
      <tab-navigation/>
    <router-view />
    </q-layout>
  </div>
</template>

<script>
import { QLayout, QToolbar, QToolbarTitle } from "quasar";
import TabNavigation from "./components/tab-navigation";
export default {
  name: "App",
  components: {
    QLayout,
    QToolbar,
    QToolbarTitle,
    TabNavigation
  }
};
</script>

<style></style>
