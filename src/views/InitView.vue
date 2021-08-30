<template>
  <v-container>
    <v-form>
      <v-text-field
        dense
        outlined
        label="DB File"
        @click="dbClicked"
        :value="dbFile"
      ></v-text-field>
      <v-text-field
        dense
        outlined
        label="Data folder"
        @click="folderClicked"
        :value="dataFolder"
      ></v-text-field>
      <v-btn dense @click="loadDB" :loading="loading">Load</v-btn>
    </v-form>
  </v-container>
</template>

<script>
import { ipcRenderer } from "electron";
import dbRequests from "../utils/db-requests";

export default {
  data() {
    return {
      dbFile: "",
      dataFolder: "",
      loading: false,
    };
  },
  methods: {
    async dbClicked() {
      let path = await ipcRenderer.invoke("choose-file", [
        { name: "Namalysator DB", extensions: ["db"] },
      ]);
      if (path) this.dbFile = path;
    },
    async folderClicked() {
      let path = await ipcRenderer.invoke("choose-folder");
      if (path) this.dataFolder = path;
    },
    async loadDB() {
      this.loading = true;
      await dbRequests.loadDatabase(this.dbFile);
      this.$emit("loaded");
      this.loading = false;
    },
  },
};
</script>

<style>
</style>