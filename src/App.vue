<template>
  <v-app class="grey lighten-4" app>
    <Navbar/>
    <v-main class="mx-4">
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>
import Navbar from '@/components/Navbar'
export default {
  name: 'App',

  components: { Navbar },

  
};
</script>
