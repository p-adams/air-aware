<template>
    <q-tabs slot="navigation">
      <q-route-tab
        slot="title"
        to="/home"
        label="Home"
      />
      <q-route-tab
        slot="title"
        to="/the-select-menus"
        label="Browse locations"
      />
      <q-route-tab
        slot="title"
        to="/the-monitor-keys"
        label="Monitor keys"
      />
    </q-tabs>
</template>
<script>
import { QLayout, QTabs, QRouteTab } from "quasar";
export default {
  name: "TabNavigation",
  components: {
    QLayout,
    QTabs,
    QRouteTab
  }
};
</script>

