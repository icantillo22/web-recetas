<template>
  <v-app-bar
    app
    :color="'#FFFFFF'"
    elevate-on-scroll
  >
    <v-container>
      <v-toolbar-title><b>
        <router-link class="color-title" to="/">KUKS FRESH</router-link>
      </b></v-toolbar-title>
    </v-container>

    <template v-slot:extension>
      <v-tabs 
        centered
        color="red"
      >
        <v-tabs-slider color="red"></v-tabs-slider>
        <v-tab to="/">Inicio</v-tab>
        <v-tab to="/about">Nosotros</v-tab>
        <v-tab to="/media">Videos</v-tab>
      </v-tabs>
    </template>

    <v-spacer></v-spacer>


    <v-btn
      fab
      dark
      small
      color="red"
      elevation="0"
    >
      <v-icon dark>{{ icons.mdiAccount }}</v-icon>
    </v-btn>

  </v-app-bar>
</template>

<script>
import { mdiAccount } from '@mdi/js';

export default {
  name: 'NavbarApp',
  data: () => ({
    icons: {
      mdiAccount
    }
  })
}
</script>

<style scoped>
  .color-title {
    color: #EF4C00;
    text-decoration: none;
  }
</style>