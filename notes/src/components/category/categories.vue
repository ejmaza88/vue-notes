<template>
    <div>
        <div v-for="(category, index) in categories">
            <span class="pointer" v-bind:key="category.id" @click="categoryItemClick(category)">{{category.name}}</span>
            <span class="pointer float-right" v-bind:key="category.id + 'x'" @click="deleteCategoryItem(index)">x</span>
        </div>

        <br />
        <form role="form" @submit.prevent="addCategory">
            <div class="form-group">
                <input class="form-control form-control-sm" type="text" placeholder="Add Category..." v-model="categoryModel.name" />
            </div>
            <button type="submit" class="btn btn-primary btn-sm">Submit</button>
        </form>
    </div>
</template>


<script>
export default {
    name: 'CategoryComponent',
    props: ['categories'],
    data() {
        return {
            categoryModel: {"id": "", "name": ""}
        }
    },
    methods:{
        categoryItemClick: function(category) {
            fetch("http://127.0.0.1:5000/api/get-data/",{
              method: "GET"
            })
            .then(response => response.json())
            .then(data => {
                this.$emit("getCategoryNotes", data);
            })
            .catch(error => {
                console.log("something went wrong: ", error);
            })
        },
        deleteCategoryItem: function(categoryIndex) {
            this.$emit("delCategory", categoryIndex)
        },
        addCategory: function() {
            this.categoryModel.id = Math.floor(Math.random() * 999999)
            this.$emit("addNewCategory", this.categoryModel)
            this.categoryModel = {"id": "", "name": ""}
        }
    }
}
</script>


<style>
.pointer {
    cursor: pointer;
}
</style>
