<template>
    <form @submit.prevent="save">
    <div class="form-group">
        <label for="exampleInputTitle">Title</label>
        <input type="text" class="form-control" id="exampleInputTitle" placeholder="Title" v-model="recipe.title">
    </div>
    <div class="form-group">
        <label for="exampleInputDes">Des</label>
        <input type="text" class="form-control" id="exampleInputDes" placeholder="Des" v-model="recipe.description">
    </div>
    <div class="form-group">
        <label for="exampleInputImage">Image</label>
        <input type="text" class="form-control" id="exampleInputImage" placeholder="Image" v-model="recipe.image">
    </div>
    {{recipe}}
    <button class="btn btn-danger">Cancle</button>
    <button type="submit" class="btn btn-primary">Save</button>
    </form>
</template>

<script>
    export default {
        data (){
            return {
                recipe: {
                    id: "",
                    title: "",
                    description: "",
                    image: ""
                }
            }
        },
        methods:{
            save () {
                this.recipe.id = Math.random()
                this.$emit("formSaved", this.recipe)
            }
        }
    }
</script>

<style scoped>

</style>