<template>
  <div>
    <v-row v-if="data.length > 0" >
        <v-col
          v-for="recipe in data" :key="recipe.idMeal"
        >
          <recipe-item :recipe-data="recipe" />
        </v-col>        
    </v-row>
    <v-row v-else>
      <v-col cols="12">
        <h3 class="text-center">No se han encontrado resultados</h3>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import recipeItem from "./recipeItem.vue"

export default {
  name: 'RecipeList',
  components: { recipeItem },
  props: {
    data: {
      type: Array,
      default: () => [],
    }
  }
}
</script>