<template>
  <q-layout ref="layout">
      <q-toolbar slot="header">
          <q-toolbar-title>Air Aware</q-toolbar-title>
          <div slot="subtitle">Monitor harmful air pollution</div>
      </q-toolbar>
     <q-tabs slot="navigation">
       <q-route-tab
          slot="title"
          to="/"
          label="Main"
        />
        <q-route-tab
          slot="title"
          to="/the-select-menus"
          label="Browse"
        />
     </q-tabs>
   
  </q-layout>
</template>
<script>
import { QLayout, QToolbar, QToolbarTitle, QTabs, QRouteTab } from "quasar";
import TheSelectMenus from "./the-select-menus";
export default {
  name: "MainPage",
  components: {
    QLayout,
    QToolbar,
    QToolbarTitle,
    QTabs,
    QRouteTab,
    TheSelectMenus
  }
};
</script>

