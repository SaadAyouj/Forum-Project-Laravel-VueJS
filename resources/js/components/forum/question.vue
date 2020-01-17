<template>
  <v-card raised id="card">
    <v-card-title primary-title>
        <div>
            <h3 class="headline mb-0">
                <router-link :to="data.path">
                    {{data.title}}
                </router-link>
            </h3>
        </div>
    </v-card-title>

    <v-card-subtitle>
        <div><span class="grey--text">{{data.created_at}}</span><b> by {{data.user}}</b></div>
    </v-card-subtitle>

    <v-card-text>
      {{data.body}}
    </v-card-text>
  </v-card>
</template>

<script>
export default {
    props:['data']
}
</script>

<style>
#card{
    margin-top: 25px;
    margin-bottom: 15px;
}
</style>
