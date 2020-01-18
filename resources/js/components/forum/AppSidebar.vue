<template>
  <v-card shaped raised class="ml-4" dark>
        <v-toolbar color="blue" dark dense class="mt-6">
            <v-toolbar-title><b>Categories</b></v-toolbar-title>
            <v-spacer></v-spacer>
            <v-icon>mdi-magnify</v-icon>
        </v-toolbar>


        <div v-for="category in categories" :key="category.id">
            <v-divider></v-divider>
            <v-list dense>
                <v-list-item>
                    <v-list-item-content>
                        <v-list-item-title><center><b>{{category.name}}</b></center></v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
            </v-list>
        </div>
  </v-card>
</template>

<script>
export default {
    data(){
        return{
            categories:{}
        }
    },
    created(){
        axios.get('/api/category')
        .then(res => this.categories = res.data.data)
        .catch(err => {
            console.error(err);
        })
    }
}
</script>

<style>

</style>
