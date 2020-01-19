<template>
  <div>
      <v-card shaped>
            <v-card-title class="subtitle-2 font-weight-bold">
                {{data.user}} &nbsp;
                <span class="caption grey--text"> said {{data.created_at}}</span>
                <v-spacer></v-spacer>
                <like :content="data"></like>
            </v-card-title>

             <edit-reply
            v-if="editing"
            :reply=data
            ></edit-reply>

            <v-card-text v-else v-html="reply"></v-card-text>

            <v-divider></v-divider>

            <div v-if="!editing">
            <v-card-actions v-if="own">
                <v-btn icon small>
                    <v-icon color="orange" @click="edit">edit</v-icon>
                </v-btn>
                <v-btn icon small>
                    <v-icon color="red" @click="destroy">delete</v-icon>
                </v-btn>
            </v-card-actions>
            </div>

      </v-card>
  </div>
</template>

<script>
import EditReply from './editReply'
import Like from '../likes/like'
export default {
    props:['data','index'],
    components:{EditReply,Like},
    data(){
        return {
            editing:false,
            beforeEditReplyBody:''
        }
    },
    computed:{
        own(){
            return User.own(this.data.user_id)
        },

        reply(){
            return md.parse(this.data.reply)
        }
    },
    created(){
        this.listen()
    },
    methods: {
        destroy(){
            EventBus.$emit('deleteReply',this.index)
        },
        edit(){
            this.editing = true,
            this.beforeEditReplyBody = this.data.reply
        },
         listen(){
            EventBus.$on('cancelEditing',(reply)=>{
                this.editing = false
                if(reply !== this.data.reply){
                    this.data.reply = this.beforeEditReplyBody
                    this.beforeEditReplyBody = ''
                 }
            })
        }
    }
}

</script>

<style>

</style>
