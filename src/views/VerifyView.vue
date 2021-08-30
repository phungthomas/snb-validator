<template>
  <v-container fluid class="pa-0">
    <v-toolbar dense color="blue">
      <v-spacer></v-spacer>
      <v-btn icon>
        <v-icon>mdi-dots-vertical</v-icon>
      </v-btn>
    </v-toolbar>

    <multipane>
      <div>asdf</div>
      <multipane-resizer></multipane-resizer>
      <div>asdf</div>
    </multipane>

    <v-navigation-drawer absolute right permanent>
      <v-list>
        <v-list-item
          dense
          link
          v-for="item in samplingMets"
          :key="item.METS_ID"
        >
          <v-list-item-content>
            <v-list-item-title>{{ item.FILENAME }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
  </v-container>
</template>

<script>
//import { ipcRenderer } from "electron";
import dbRequests from "../utils/db-requests";
import { Multipane, MultipaneResizer } from "vue-multipane";

export default {
  components: {
    Multipane,
    MultipaneResizer,
  },
  data() {
    return {
      mets: [],
      samplingMets: [],
      selectedMets: null,
    };
  },
  computed: {},
  mounted() {
    this.mets = dbRequests.mets;
    this.samplingMets = dbRequests.samplingMets;
  },
  methods: {},
};
</script>

<style>
</style>