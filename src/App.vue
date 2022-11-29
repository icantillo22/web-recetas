<template>
  <v-app>  
    <menu-app />
    <v-main>
      <router-view/>
    </v-main>
  </v-app>
</template>

<style scoped>
  .bg-main {
    background-color: #FFFFFF;
  }

</style>

<script>
import MenuApp from '@/components/app/MenuApp.vue';

export default {
  components: { MenuApp },
  name: 'App',

  data: () => ({
    //
  }),
};
</script>
