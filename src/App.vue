<template>
  <v-app>
    <navbar></navbar>
    <router-view></router-view>
  </v-app>
</template>

<script>
import Navbar from './views/Navbar'

export default {
  name: 'App',
  components: {
    Navbar
  },
  data () {
    return {
      title: process.env.VUE_APP_TITLE
    }
  }
}
</script>
