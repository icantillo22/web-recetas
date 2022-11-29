<template>
  <v-dialog
    :value="isLoading"
    transition="dialog-bottom-transition"
    persistent
    width="700"
  >
    <v-container fluid style="background-color: #FFFAFC;">
      <v-row>
        <v-col>
          <v-img
            :src="gifLoading"
          >
          </v-img>
        </v-col>
      </v-row>
    </v-container>
  </v-dialog>
</template>

<script>
import gifLoading from '@/assets/gif-loading.gif'
export default {
  name: 'LoadingModal',
  props: {
    isLoading: {
      type: Boolean,
      default: false,
    }
  },  
  data: () => ({
    gifLoading
  })
}
</script>

<style>

</style>