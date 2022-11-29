<template>
  <div>
    <v-container>
      <v-row>
          <v-col>
            <banner-page
              :url="recipe.strMealThumb"
            />
          </v-col>
      </v-row>
      <v-row>
        <v-col>
          <v-icon>{{ icons.mdiClockTimeThreeOutline }}</v-icon> 20-30
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <h2 class="title-recipe">{{ recipe.strMeal }}</h2>
        </v-col>
        <v-col class="d-flex justify-end">        
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
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <v-rating
              color="red"
              background-color="red"
              readonly
              size="18"
              :value="4.5"
              dense
              half-increments
            ></v-rating>
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <v-chip v-for="tag in tags" :key="tag" class="mx-1 bg-chip">{{ tag }}</v-chip>
        </v-col>
      </v-row>
      <v-row>
        <v-col 
          class="text-justify mx-auto"
          cols="12"
          md="10"
          lg="8"
        >
          <p class="text-recipe">
            {{ recipe.strInstructions }}
          </p>
        </v-col>
      </v-row>      
    </v-container>
    
    <loading :isLoading="isLoading" />
  </div>
</template>

<script>
import { mdiCardsHeart, mdiCardsHeartOutline, mdiClockTimeThreeOutline } from '@mdi/js';
import bannerPage from '@/components/generals/bannerPage.vue'
import Loading from '@/components/generals/Loading.vue';

export default {
  name: 'RecipeView',
  components: { 
    bannerPage, 
    Loading, 
  },

  async created() {
    this.isLoading = true;
    await this.getDataById();
    this.isLoading = false;
  },

  data: () => ({
    isLoading: false,
    like: false,
    icons: {
      mdiCardsHeart,
      mdiCardsHeartOutline,
      mdiClockTimeThreeOutline 
    },
    recipe: {},
    tags: []
  }),

  methods: {
    async getDataById() {
      try {
        this.recipes = []

        this.isLoading = true;
        const idRecipe = this.$route.params.id;
        const req = await fetch(`https://www.themealdb.com/api/json/v1/1/lookup.php?i=${idRecipe}`);
        const res = await req.json()
        this.isLoading = false;

        if(res?.meals.length <= 0) {
          return false;
        }

        res.meals.forEach(recipe => {
          this.recipe = recipe
        });

        this.tags = this.recipe?.strTags.split(',')

        return true

      } catch (error) {
        console.log(error)
      }
    }
  }
}
</script>

<style scoped>
  .title-recipe {
    text-decoration: none;
    color: #B30733;
  }

  .bg-chip {
    background-color: #F6F7F8 !important;
  }

  .text-recipe {
    color: #B30735;
  }
</style>