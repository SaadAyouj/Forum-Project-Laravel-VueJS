<template>
    <v-container fluid>
        <v-card>
            <v-container>
            <v-form @submit.prevent="update">
                <v-text-field
                v-model="form.title"
                label="Title"
                type="text"
                required
            ></v-text-field>

            <vue-simplemde v-model="form.body" />

            <v-card-actions>
                <v-btn icon small type="submit">
                    <v-icon color="blue">
                        save
                    </v-icon>
                </v-btn>

                <v-btn icon small @click="cancel">
                    <v-icon color="red">
                        cancel
                    </v-icon>
                </v-btn>
            </v-card-actions>
            </v-form>
            </v-container>
        </v-card>
    </v-container>
</template>

<script>
export default {
    props:['data'],
    data(){
        return {
            form:{
                title:null,
                body:null
            }
        }
    },
    methods:{
        cancel(){
            EventBus.$emit('cancelEditing')
        },
        update(){
            axios.patch(`/api/question/${this.form.slug}`,this.form)
            .then(res => {this.cancel()
            this.$noty.success("Your question has been <b>updated</b>!")})
            .catch(err => {
                console.error(err);
                this.$noty.error("Oops, something went wrong!")
            })
        }
    },
    mounted(){
        this.form=this.data
    }

}
</script>

<style>

</style>
