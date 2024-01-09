<template>
  <v-app>




    <HomeView />

  </v-app>
</template>

<script>
import HomeView from './views/HomeView.vue';

export default {
  components: { HomeView },
  name: 'App',

  data: () => ({
    //
  }),
};
</script>
