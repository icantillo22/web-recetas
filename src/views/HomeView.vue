<template>
  <div>
    <v-container>
      <v-row class="mt-3">
        <v-col>
          <h1 class="text-center">
              "People who loves to eat are always Best People"<br />
              <span class="text-right color-title">JULIA CHILD</span>
          </h1>
        </v-col>
      </v-row>
      <v-row>
        <v-col
        >
          <banner-page 
            :url="logoBanner"
            text="Encuentra Las Mejores<br/> Recetas Para Ti<br/> Y Tu Familia." 
          />
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <div class="mx">
            <h2 class="color-title-seccion">RECETAS</h2>
          </div>
        </v-col>
        <v-col
          class="ml-auto"
          cols="9"
          sm="8"
          md="6"
          lg="4"
        >
          <v-text-field
            placeholder="Search by name"
            filled
            rounded
            dense
            :append-icon="icons.mdiMagnify"
            color="red"
            v-model="search"
          ></v-text-field>
        </v-col>
      </v-row>
      <!-- CATEGORIES -->
      <v-row>
        <v-col 
          cols="12"
          class="scroll-chip"
        >
          <v-chip-group
            color="red"   
            mandatory
            v-model="selectedCategory"
          >
            <v-chip 
              v-for="category in categories" 
              :key="category" 
              class="mx-2 bg-chip"
              :value="category"
              @click="getRecipes"
            >
              {{category}}
            </v-chip>
          </v-chip-group>
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <recipe-list :data="filterRicepes" />
        </v-col>
      </v-row>
    </v-container>
    <loading :isLoading="isLoading" />
  </div>
</template>

<script>
import { mdiMagnify } from '@mdi/js';
import RecipeList from '@/components/generals/recipeList.vue'
import BannerPage from '@/components/generals/bannerPage.vue';
import Loading from '@/components/generals/Loading.vue';
import logoBanner from '@/assets/logo-banner.jpg'


  export default {
    name: 'HomeView',

    components: {
      RecipeList,
      BannerPage,
      Loading,
    },

    computed: {
      filterRicepes() {

        const newArray = this.recipes.filter( (recipe) => recipe.strMeal.toLowerCase().includes(this.search.toLocaleLowerCase()));
        return newArray
      },
    },

    data: () => ({
      isLoading: false,
      logoBanner,
      icons: {
        mdiMagnify
      },
      search: '',
      selectedCategory: '',
      categories: [],
      recipes: [],
    }),

    async created() {
      this.isLoading = true;
      await this.getCategories();
      await this.getRecipes();
      this.isLoading = false;
    },

    methods: {
      async getCategories(){
        try {
          const req = await fetch('https://www.themealdb.com/api/json/v1/1/list.php?c=list');
          const res = await req.json()

          if(res?.meals.length <= 0) {
            return false;
          }

          res.meals.forEach(category => {
            this.categories.push(category.strCategory)
          });

          this.selectedCategory = this.categories[0];

          return true

        } catch (error) {
          console.log(error)
        }
      },
      async getRecipes(){
        try {
          this.recipes = []

          this.isLoading = true;
          const req = await fetch(`https://www.themealdb.com/api/json/v1/1/filter.php?c=${this.selectedCategory}`);
          const res = await req.json()
          this.isLoading = false;

          if(res?.meals.length <= 0) {
            return false;
          }

          res.meals.forEach(recipe => {
            this.recipes.push(recipe)
          });

          return true

        } catch (error) {
          console.log(error)
        }
      },
    },
  }
</script>

<style scoped>
  .color-title-seccion {
    color: #B30733;
  }

  .color-title {
    color: #EF4C00;
  }
  .bg-chip {
    background-color: #F6F7F8 !important;
  }

  .scroll-chip {
    overflow-x: auto;
  }

</style>
