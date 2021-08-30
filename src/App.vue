<template>
  <v-app>
    <v-main>
      <init-view v-if="!dbLoaded" @loaded="dbLoaded = true" />
      <verify-view v-else @unload="dbLoaded = false" />
    </v-main>
  </v-app>
</template>

<script>
import InitView from "./views/InitView.vue";
import VerifyView from "./views/VerifyView.vue";

export default {
  name: "App",

  components: {
    InitView,
    VerifyView,
  },

  data: () => ({
    dbLoaded: false,
  }),
  methods: {},
};
</script>
