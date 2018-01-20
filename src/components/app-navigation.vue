<template>
    <q-tabs slot="navigation" class="bg-secondary">
      <q-route-tab
        slot="title"
        to="/"
        label="Home"
      />
      <q-route-tab
        slot="title"
        to="/browse-location"
        label="Browse your location"
      />
      <q-route-tab
        slot="title"
        to="/browse"
        label="Browse all locations"
      />
    </q-tabs>
</template>
<script>
import { QLayout, QTabs, QRouteTab } from "quasar";
export default {
  name: "AppNavigation",
  components: {
    QLayout,
    QTabs,
    QRouteTab
  }
};
</script>
