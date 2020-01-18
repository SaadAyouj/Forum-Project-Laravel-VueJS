<template>
<v-container>
    <v-card tile>
        <v-container fluid>
            <div>
                <v-card-title>

                <div class="headline">
                    {{data.title}}
                </div>

                <v-spacer></v-spacer>

                <v-btn color="teal white--text">
                    {{data.reply_count}} Replies
                </v-btn>
                </v-card-title>

                <v-card-subtitle>
                    <div><span class="grey--text">{{data.created_at}}</span>
                    by {{data.user}}</div>
                </v-card-subtitle>
            </div>

            <v-card-text v-html="body"></v-card-text>

            <v-card-actions v-if="own">
            <v-btn icon small @click="edit">
                <v-icon color="orange">edit</v-icon>
            </v-btn>
            <v-btn icon small @click="destroy">
                <v-icon color="red">delete</v-icon>
            </v-btn>
        </v-card-actions>
        </v-container>
    </v-card>
    </v-container>
</template>

<script>
export default {
    props:['data'],
    data(){
        return{
            own: User.own(this.data.user_id),
        }
    },
    computed:{
        body(){
            return md.parse(this.data.body)
        }
    },
    methods:{
        destroy(){
            axios.delete(`/api/question/${this.data.slug}`)
            .then(res => {this.$router.push('/forum')
            this.$noty.warning("Your question has been <b>deleted</b>")})
            .catch(error => console.log(error.reponse.data))
        },
        edit(){
            EventBus.$emit('startEditing')
        }
    }
}
</script>

<style>

</style>
