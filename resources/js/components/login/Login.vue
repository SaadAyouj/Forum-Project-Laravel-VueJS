<template>
<v-container>
  <v-form @submit.prevent="login">
    <v-container>
      <v-row>
        <v-col
          cols="12"
          md="4"
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
          md="4"
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
          md="4"
        >
            <v-btn
            color="green"
            type="submit"
            >Login</v-btn>
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
    methods:{
        login(){
            User.login(this.form)
        }
    }
}
</script>

<style>

</style>
