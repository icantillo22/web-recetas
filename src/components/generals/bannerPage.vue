<template>
  <v-parallax
    class="rounded-xl"
    :src="(url.length <= 0 ? gifLoading : url)"
    dark
  >
    <v-container>
      <v-row>
        <v-col>
          <h1 v-show="text.length <= 0" style="visibility: hidden;">
            Encuentra Las Mejores<br/> Recetas Para Ti<br/> Y Tu Familia.
          </h1>
          <h1 v-show="text.length > 0" v-html="text"></h1>
        </v-col>
      </v-row>
      <v-row class="mt-10">
        <v-col>
          <v-btn :color="'#B30733'" dark class="mx-3 ma-1 px-4 py-8">
            <v-icon size="45">{{ icons.mdiApple }}</v-icon>
            Download on the <br/> App Store
          </v-btn>
          <v-btn color="red" dark class="mx-3 ma-1 px-4 py-8">
            <v-icon size="45">{{ icons.mdiGooglePlay }}</v-icon>
            Get in on <br />
            Play Store
          </v-btn>
        </v-col>
      </v-row>
    </v-container>
  </v-parallax>   
</template>

<script>
import gifLoading from '@/assets/gif-loading.gif'
import { mdiGooglePlay, mdiApple } from '@mdi/js';

export default {
  name: 'BannerPage',
  props: {
    text: {
      type: String,
      default: '',
    },
    url: {
      type: String,
      default: '',
    }
  },
  data: () => ({
    gifLoading,
    icons: {
      mdiGooglePlay,
      mdiApple,
    },
  })
}
</script>

<style>

</style>