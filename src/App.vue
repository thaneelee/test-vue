<template>
  <div id="app">
    <header-component></header-component>
    <div class="container">
      <!-- Content here -->
      <h1 v-if="isNewRecipe">Crane Toreba</h1>
      <recipe-form  v-if="isNewRecipe" @formSaved="saveRecipedList"></recipe-form>
      <div class="row">
        <div class="col">
          <button type="button" class="btn btn-outline-success float-right" @click="isNewRecipe = !isNewRecipe" >Success</button>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <input type="text" class="form-control" v-model="searchTitle"  />
        </div>
      </div>
      <div class="row">
        <div class="col" v-for="recipe in filterList" :key="recipe.id">
          <recipecard @recipeDeleted="actionDeleted" :recipe="recipe"></recipecard>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import HeaderComponent from './components/Header.vue'
import Recipecard from './components/Recipecard.vue'
import RecipeForm from './components/RecipeForm.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    HeaderComponent,
    Recipecard,
    RecipeForm
  },
  data(){
    return {
      isNewRecipe: false,
      recipes: [
      //   {
      //   id: "1",
      //   title: "Toreba 1",
      //   description: "Toreba Des 2",
      //   image: "http://en.play.toreba.net/en/images/teaser/en/img_ogp.jpg"
      // },
      // {
      //   id: "2",
      //   title: "Toreba 2",
      //   description: "Toreba Des 2",
      //   image: "https://i.ytimg.com/vi/JrhZrio0dUA/maxresdefault.jpg"
      // },
      // {
      //   id: "3",
      //   title: "Toreba 3",
      //   description: "Toreba Des 3",
      //   image: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT_-d2b20dAhfxDGWZ_33yEkAvZNrD6LkUSnwK2x5ZKAxEbHHR2"
      // }
      ],
      searchTitle: ""
    }
  },
  computed: {
    filterList() {
      return this.recipes.filter(recipe => {
        console.log(recipe.title.toLowerCase().indexOf(this.searchTitle.toLowerCase()))
        return recipe.title.toLowerCase().indexOf(this.searchTitle.toLowerCase()) > -1
      })
    }
  },
  mounted (){
    if(localStorage.getItem('recipes')){
      this.recipes = JSON.parse(localStorage.getItem('recipes'))
    }
  },
  watch:{
    recipes:{
      handler () {
        localStorage.setItem('recipes', JSON.stringify(this.recipes))
      },
      deep: true
    }
  },
  methods:{
    saveRecipedList(recipe){
      this.isNewRecipe = false
      this.recipes.push(recipe)
    },
    actionDeleted(recipeId){
      const index = this.recipes.findIndex((value) => value.id === recipeId) 
      this.recipes.splice(index,1)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
