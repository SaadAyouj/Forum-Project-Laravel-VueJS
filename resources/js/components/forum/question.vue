<template>
  <v-card raised id="card" dark>
    <v-card-title primary-title>
        <div>
            <h3 class="headline mb-0">
                <router-link :to="data.path" id="color">
                    {{data.title}}
                </router-link>
            </h3>
        </div>
    </v-card-title>

    <v-card-subtitle>
        <div><span class="grey--text">{{data.created_at}}</span><b> by {{data.user}}</b></div>
    </v-card-subtitle>

    <v-card-text v-html="body"></v-card-text>
  </v-card>
</template>

<script>
export default {
    props:['data'],
    computed:{
        body(){
            return md.parse(this.data.body)
        }
    },
}
</script>

<style>
#card{
    margin-top: 25px;
    margin-bottom: 15px;
}
#color{
    color: rgb(21, 142, 255);
    font-weight: bold;
}
</style>
