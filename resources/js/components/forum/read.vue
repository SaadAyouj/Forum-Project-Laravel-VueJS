<template>
    <div v-if="question">
        <edit-question
        v-if="editing"
        :data = question
        ></edit-question>

        <show-question
        v-else
        :data = question
        ></show-question>

        <replies :question="question"></replies>
        <new-reply v-if="loggedIn" :questionSlug = "question.slug"></new-reply>

        <div v-else class="mb-10 mt-4"><b><center>
      <router-link to="/login">Login in to Reply</router-link>
        </center></b></div>

    </div>

</template>

<script>

import ShowQuestion from './ShowQuestion'
import EditQuestion from './editQuestion'
import Replies from '../reply/replies'
import newReply from '../reply/newReply'
export default {
    components:{ShowQuestion,EditQuestion,Replies,newReply},
    data(){
        return{
            question:null,
            editing:false
        }
    },
    created(){
        this.listen()
        this.getQuestion()
    },
    computed:{
        loggedIn(){
            return User.loggedIn()
        }
    },
    methods:{
        listen(){
            EventBus.$on('startEditing', ()=>{
                this.editing = true
            })

            EventBus.$on('cancelEditing', ()=>{
                this.editing = false
            })
        },
        getQuestion(){
            axios.get(`/api/question/${this.$route.params.slug}`)
        .then(res => this.question = res.data.data)
        .catch(err => {
            console.error(err);
        })
        }
    }
}
</script>

<style>

</style>
