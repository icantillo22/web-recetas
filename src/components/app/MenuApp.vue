<template>
  <div v-if="isMobile">
    <sidebar />
  </div>
  <div v-else>
    <navbar />
  </div>
</template>

<script>
import Navbar from '@/components/app/Navbar.vue';
import Sidebar from '@/components/app/Sidebar.vue';

export default {
  name: 'MenuApp',
  components: { Navbar, Sidebar },
  computed: {
    isMobile () {
      console.log(this.$vuetify.breakpoint.name.includes('xs', 'sm'))
      if (this.$vuetify.breakpoint.name.includes('xs', 'sm')) {
        return true
      } 

      return false;
    },
  },
}
</script>

<style>

</style>