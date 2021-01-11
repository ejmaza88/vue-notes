<template>
  <div id="app">
    <navbar-component />

    <div class="container-fluid">
      <div class="row">
        <div class="col-sm-2">
          <category-component v-bind:categories="categories" @getCategoryNotes="updateCategoryArray" @addNewCategory="addNewCategoryToArray" @delCategory="deleteCategoryFromArray"/>
        </div>

        <div class="col-sm-10">
          <note-component v-bind:notes="notes" />
        </div>
      </div>
    </div>

  </div>
</template>


<script>
import NavbarComponent from "./components/navbar"
import CategoryComponent from "./components/category/categories"
import NoteComponent from "./components/note/notes"

export default {
  name: 'app',
  created: function () {
    fetch("http://127.0.0.1:5000/api/get-data/")
      .then(response => response.json())
      .then(data => {
        console.log(data)
        this.categories = data.categories;
      })
      .catch(error => {
        console.log("something went wrong: ", error);
      })
  },
  data () {
    return {
      categories: [],
      notes: [
        "Mazda",
        "Honda",
        "BMW"
      ]
    }
  },
  components: {
    "navbar-component": NavbarComponent,
    "category-component": CategoryComponent,
    "note-component": NoteComponent,
  },
  methods: {
    updateCategoryArray: function(params) {
      console.log(params.notes);
    },
    addNewCategoryToArray: function(params) {
      this.categories.push(params);
    },
    deleteCategoryFromArray: function(categoryIndex) {
      if(confirm("Delete Category?")) {
        this.categories.splice(categoryIndex, 1);
        console.log(this.categories)
      }
    }
  }
}
</script>


<style>
</style>