<template>
    <q-tabs slot="navigation">
      <q-route-tab
        slot="title"
        to="/"
        label="Home"
      />
      <q-route-tab
        slot="title"
        to="/browse"
        label="Browse locations"
      />
      <q-route-tab
        slot="title"
        to="/featured"
        label="Monitor keys"
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
