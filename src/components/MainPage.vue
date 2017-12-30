<template>
  <q-layout>
      <q-toolbar>
          <q-toolbar-title>Air Aware</q-toolbar-title>
          <div slot="subtitle">Monitor harmful air pollution</div>
      </q-toolbar>
     <the-select-menus/>
   
  </q-layout>
</template>
<script>
import { QLayout, QToolbar, QToolbarTitle } from "quasar";
import TheSelectMenus from "./the-select-menus";
export default {
  name: "MainPage",
  components: {
    QLayout,
    QToolbar,
    QToolbarTitle,
    TheSelectMenus
  }
};
</script>

