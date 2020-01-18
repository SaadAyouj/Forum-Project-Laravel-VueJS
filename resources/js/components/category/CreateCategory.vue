<template>
  <v-container>
      <v-form ml-5 mr-5 mt-3 @submit.prevent="submit">
          <v-text-field
                v-model="form.name"
                label="Category Name"
                type="text"
                required
            ></v-text-field>

            <v-btn id="btncate" type="submit" color="yellow darken-4" v-if="editSlug">Update</v-btn>
            <v-btn id="btncate" type="submit" color="green darken-1" v-else>Create</v-btn>
      </v-form>

    <v-card>
        <v-toolbar color="blue" dark dense>
          <v-toolbar-title>Categories</v-toolbar-title>
        </v-toolbar>

        <v-list>
            <div mt-4 v-for="(category, index) in categories" :key="category.id">
                <v-list-item>

                <v-list-item-action>
                    <v-btn icon small @click="edit(index)">
                        <v-icon color="orange">edit</v-icon>
                    </v-btn>
                </v-list-item-action>

                <v-list-item-content>
                    <v-list-item-title>
                        {{category.name}}
                    </v-list-item-title>
                </v-list-item-content>

                <v-list-item-action>
                    <v-btn icon small @click="destroy(category.slug, index)">
                        <v-icon color="red">delete</v-icon>
                    </v-btn>
                </v-list-item-action>
            </v-list-item>
            <v-divider></v-divider>
            </div>
        </v-list>
      </v-card>
  </v-container>
</template>

<script>
export default {
    data(){
        return{
            form:{
                name:null
            },
            categories:{},
            editSlug:null
        }
    },
    created(){
        axios.get('/api/category')
        .then(res => this.categories = res.data.data)
    },
    methods:{
        submit(){
            this.editSlug ? this.update() : this.create()
        },
        create(){
            if(!User.admin()){
                this.$router.push('/forum')
            }

            axios.post('/api/category',this.form)
            .then(res => {this.categories.unshift(res.data)
            this.form.name=null
            })
            .catch(err => {
                console.error(err);
            })
        },
        update(){
            axios.patch(`/api/category/${this.editSlug}`,this.form)
            .then(res => {this.categories.unshift(res.data)
            this.form.name=null
            this.editSlug=null
            })
            .catch(err => {
                console.error(err);
            })
        },
        destroy(slug, index){
            axios.delete(`/api/category/${slug}`)
            .then(res => this.categories.splice(index,1))
        },
        edit(index){
            this.form.name=this.categories[index].name
            this.editSlug=this.categories[index].slug
            this.categories.splice(index,1)
        }
    }
}
</script>

<style>
    #btncate{
        color:white;
    }
    .v-card{
        margin-top: 20px;
    }
</style>
