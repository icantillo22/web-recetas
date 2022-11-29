<template>
  <v-card
    class="mx-auto my-12 rounded-xl"
    max-width="374"   
    elevation="0"
    outlined    
  >
    <router-link :to="`/recipe/${recipeData.idMeal}`">
      <v-img
        class="rounded-t-xl"
        height="200"
        :lazy-src="gifLoading"
        :src="recipeData.strMealThumb"
      ></v-img>
    </router-link>

    <div class="px-3 pb-4">  
      <div class="d-flex align-center justify-space-between px-2">
        <router-link class="card-title" :to="`/recipe/${recipeData.idMeal}`">
          <h3>{{ recipeData.strMeal }}</h3>
        </router-link>
  
        <v-btn
          fab
          small
          elevation="0"
          icon
          @click="like = !like"
        >
          <v-icon color="red" v-show="like === true">{{ icons.mdiCardsHeart }}</v-icon>
          <v-icon color="red" v-show="like === false">{{ icons.mdiCardsHeartOutline }}</v-icon>
        </v-btn>
      </div>

      <div class="d-flex align-center pl-1">
        <v-rating
          color="red"
          background-color="red"
          readonly
          size="17"
          :value="4.5"
          dense
          half-increments
        ></v-rating>
        (4.5)
      </div>
  
      <div class="mt d-flex align-center justify-end pt-3">
        <v-icon class="mr-2">{{ icons.mdiClockTimeThreeOutline }}</v-icon> 20-30
      </div>
    </div>
  </v-card>
</template>

<script>
import { mdiCardsHeart, mdiCardsHeartOutline, mdiClockTimeThreeOutline   } from '@mdi/js';
import gifLoading from '@/assets/gif-loading.gif'

export default {
  name: 'RecipeItem',
  props: {
    recipeData: {
      type: Object,
      default: Object,
    },
  },
  data: () => ({
    gifLoading,
    icons: {
      mdiCardsHeart,
      mdiCardsHeartOutline,
      mdiClockTimeThreeOutline 
    },
    like: false
  })
}
</script>

<style scoped>

  .card-title {
    text-decoration: none;
    color: #B30733;
  }
  .bg-chip {
    background-color: #F6F7F8 !important;
  }
</style>