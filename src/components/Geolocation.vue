<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-img
          :src="require('../assets/logo.png')"
          class="my-3"
          contain
          height="200"
        />
      </v-col>

      <v-col class="mb-4">
        <h1 class="display-2 font-weight-bold mb-3">
          Geolocation PWA
        </h1>

        <p class="subheading font-weight-regular">
          This simple offline PWA tracks your geolocation.
          <br>please join the mastacoders Discord community!
          <a
            href="https://discord.gg/DMbMmQvvQh"
            target="_blank"
          >Discord Community</a>
        </p>
      </v-col>

      <v-col
        class="mb-5"
        cols="12"
      >
        <h2 class="headline font-weight-bold mb-3" v-if="!isTracking">
          Ready?
        </h2>
        <v-row justify="center" v-if="isTracking">
          <div> Latitude: {{position.lat}}
            <br />
            Longitude: {{position.long}}
          </div>
          <div v-if="position.speed !== null">Speed: {{position.speed}} m/s
            <br />
          </div>
          <div v-if="position.heading !== null">Heading: {{position.heading}} degrees
            <br />
          </div>
          <div v-if="position.altitude !== null">Altitude: {{position.altitude}} meters
            <br />
          </div>
        </v-row>
        <v-row justify="center">
          <v-btn v-on:click="startTracking" v-if="!isTracking">Track Location</v-btn>
          <v-btn color="red" v-on:click="stopTracking" v-else>Stop Tracking</v-btn>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  export default {
    name: 'Geolocation',

    data: () => ({
      isTracking: false,
      position: {}
    }),
    methods: {
      startTracking: function () {
        if(!navigator.geolocation) {
          alert('Geolocation is not supported by your browser');
        } else {
          navigator.geolocation.getCurrentPosition(this.success, this.error);
          this.isTracking = true
        }
      },
      stopTracking: function () {
        this.isTracking = false
      },
      success: function (position) {
        this.position.lat  = position.coords.latitude
        this.position.long = position.coords.longitude
        this.position.speed = position.coords.speed
        this.position.altitude = position.coords.altitude
        this.position.heading = position.coords.heading

      },
      error: function () {
        alert('Unable to retrieve your location')
      }
    }
  }
</script>
