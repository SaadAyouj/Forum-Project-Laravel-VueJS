<template>
<v-container>
  <v-form @submit.prevent="login">
    <v-container>
      <v-row>
        <v-col
          cols="12"

        >
          <v-text-field
            v-model="form.email"
            label="E-mail"
            type="email"
            required
          ></v-text-field>
        </v-col>

         <v-col
          cols="12"

        >
          <v-text-field
            v-model="form.password"
            label="Password"
            type="password"
            required
          ></v-text-field>
        </v-col>

        <v-col
          cols="12"

        >
            <v-btn
            color=#03a9f4
            type="submit"
            class="white--text"
            >Login</v-btn>

            <router-link to="/signup">
                <v-btn
                color=#8bc34a
                class="white--text"
                >Sign Up</v-btn>
            </router-link>

        </v-col>
      </v-row>
    </v-container>
  </v-form>
  </v-container>
</template>

<script>
export default {
    data(){
        return {
            form :{
                email:null,
                password:null
            }
        }
    },
    created(){
       if(User.loggedIn()){
           this.$router.push({name:'forum'})

       }
    },
    methods:{
        login(){
            User.login(this.form)
            this.$noty.info("Welcome, nice to see you again with us!")
        }
    }
}
</script>

<style>

</style>
