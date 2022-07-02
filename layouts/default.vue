<template>
  <v-app>
    <v-app-bar :clipped-left="clipped" fixed app >
      <h2>{{title}}</h2>
      <v-icon large color="white">mdi-bookshelf</v-icon>
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-footer :absolute="!fixed" app>
      <span>&copy; Sudhinee B.</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'บ้านนายดิน',
    }
  },
}
</script>
