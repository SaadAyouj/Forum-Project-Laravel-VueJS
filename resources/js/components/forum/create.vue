<template>
<v-container>
  <v-form @submit.prevent="create">
      <v-row>
        <v-col
          cols="12"

        >
          <v-text-field
            v-model="form.title"
            label="Title"
            type="text"
            required
          ></v-text-field>
        </v-col>

        <v-col
          cols="12"

        >
        <v-autocomplete
          label="Category"
          :items="categories"
          v-model="form.category_id"
          item-text="name"
          item-value="id"
        ></v-autocomplete>
        </v-col>

         <v-col
          cols="12"

        >
          <vue-simplemde v-model="form.body" />
         </v-col>

        <v-col
          cols="12"

        >
            <v-btn
            color=blue
            type="submit"
            class="white--text"
            >Post</v-btn>

        </v-col>
      </v-row>
  </v-form>
  </v-container>
</template>

<script>
export default {
    data(){
        return{
            form:{
                title: null,
                category_id: null,
                body: null
            },
            categories: [],
            errors:{}
        }
    },
    created(){
        axios.get('/api/category')
            .then(res => this.categories = res.data.data)
    },
    methods:{
        create(){
            axios.post('/api/question', this.form)
            .then(res => {
                this.$router.push(res.data.path)
                this.$noty.success("Your question has been <b>created</b>!")
                })
            .catch(error => {this.errors = error.response.data.error
            this.$noty.error("Oops, something went wrong!")})
        }
    }
}
</script>

<style>

</style>
