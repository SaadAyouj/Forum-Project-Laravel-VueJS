<template>
  <v-container>
        <vue-simplemde v-model="body" />
        <v-btn dark @click="submit">
          <v-icon color="green">done</v-icon>
          &nbsp;Reply
        </v-btn>
  </v-container>
</template>

<script>
export default {
    props:['questionSlug'],
    data(){
        return{
            body:null
        }
    },
    methods:{
        submit(){
            axios.post(`/api/question/${this.questionSlug}/reply`,{body:this.body})
            .then(res => {
                this.body = ''
                EventBus.$emit('newReply',res.data.reply)
                this.$noty.success("You posted a new <b>reply</b>!")
                window.scrollTo(0,0)
            })
        }
    }
}
</script>

<style>

</style>
