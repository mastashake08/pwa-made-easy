<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src='./assets/logo.png'
          transition="scale-transition"
          width="40"
        />
      </div>

    </v-app-bar>

    <v-main>
      <Geolocation/>
    </v-main>
  </v-app>
</template>

<script>
import Geolocation from './components/Geolocation';

export default {
  name: 'App',

  components: {
    Geolocation,
  },

  data: () => ({
    //
  }),
};
</script>
