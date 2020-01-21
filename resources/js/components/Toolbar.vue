<template>
  <div>
    <v-toolbar dark>
      <v-toolbar-title>
          <router-link class="white--text" to="/">S.A Forum</router-link>
      </v-toolbar-title>

      <v-spacer></v-spacer>

      <app-notification></app-notification>

      <div>

          <router-link
            v-for="item in items"
            :key="item.title"
            :to="item.to"
            v-if="item.show">
                <v-btn text>{{item.title}}</v-btn>
          </router-link>

      </div>

    </v-toolbar>
  </div>
</template>

<script>
import AppNotification from './AppNotification'
export default {
    components:{AppNotification},
    data(){
        return {
            items: [
                {'title' : 'Forum', to:'/forum',show:true},
                {'title' : 'Ask a Question', to:'/ask',show: User.loggedIn()},
                {'title' : 'Create a Category', to:'/category',show: User.admin()},
                {'title' : 'Login', to:'/login',show: !User.loggedIn()},
                {'title' : 'Logout', to:'/logout',show: User.loggedIn()},
            ]
        }
    },
    created(){
        EventBus.$on('logout', () => {
            User.logout()
        })
    }

}
</script>

<style>

</style>
