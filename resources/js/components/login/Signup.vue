<template>
  <v-container>
  <v-form @submit.prevent="signup">
    <v-container>
      <v-row>
        <v-col
          cols="12"

        >
          <v-text-field
            v-model="form.name"
            label="Name"
            type="text"
            required
          ></v-text-field>
          <span class="red--text" v-if="errors.name">{{errors.name[0]}}</span>
        </v-col>

        <v-col
          cols="12"

        >
          <v-text-field
            v-model="form.email"
            label="E-mail"
            type="email"
            required
          ></v-text-field>
            <span class="red--text" v-if="errors.email">{{errors.email[0]}}</span>

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
          <span class="red--text" v-if="errors.password">{{errors.password[0]}}</span>
        </v-col>

        <v-col
          cols="12"

        >
          <v-text-field
            v-model="form.password_confirmation"
            label="Confirm Password"
            type="password"
            required
          ></v-text-field>
        </v-col>

        <v-col
          cols="12"

        >
            <v-btn
            color=#8bc34a
            type="submit"
            class="white--text"
            >Sign up</v-btn>

            <router-link to="/login">
                <v-btn
                color=#03a9f4
                class="white--text"
                >Login</v-btn>
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
        return{
            form :{
                name:null,
                email:null,
                password:null,
                password_confirmation:null
            },
            errors:{}
        }
    },
    created(){
       if(User.loggedIn()){
           this.$router.push({name:'forum'})
       }
    },
    methods:{
        signup(){
            axios.post('/api/auth/signup',this.form)
            .then(res => {
                User.responseAfterLogin(res)
                this.$router.push({name:'forum'})
                this.$noty.info("Welcome to my forum, your account has been successfully created !")
                })
            .catch(error => {this.errors = error.response.data.errors
            this.$noty.error("Oops, something went wrong!")})
        }
    }
}
</script>

<style>
a {
    text-decoration: none;
}
</style>
