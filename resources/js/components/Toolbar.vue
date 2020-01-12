<template>
  <div>
    <v-toolbar>
      <v-toolbar-title>Forum F.A</v-toolbar-title>

      <v-spacer></v-spacer>

      <div>
          <router-link to="/forum">
            <v-btn text>Forum</v-btn>
          </router-link>
            <v-btn text>Ask a Question</v-btn>
            <v-btn text>Create Your Category</v-btn>
          <router-link to="/login">
                <v-btn text>Login</v-btn>
          </router-link>

      </div>

    </v-toolbar>
  </div>
</template>

<script>
export default {

}
</script>

<style>

</style>
