<template>

    <div class="text-center">
        <v-menu offset-y>
        <template v-slot:activator="{ on: menu }">
            <v-tooltip bottom>
            <template v-slot:activator="{ on: tooltip }">
                <v-btn icon v-on="{ ...tooltip, ...menu }">
                    <v-badge
                        bordered
                        overlap
                        left
                        color="teal"
                        :content="unreadCount"
                    >
                        <v-icon :color="color">add_alert</v-icon>
                    </v-badge>

            </v-btn>
            </template>
            <span>Your Notifications</span>
            </v-tooltip>
        </template>
        <v-list>
            <v-list-item v-for="item in unread" :key="item.id">
                <router-link :to="item.path">
                    <v-list-item-title @click="readIt(item)">New reply on "{{item.question}}" from {{item.replyBy}}</v-list-item-title>
                </router-link>
            </v-list-item>

            <v-divider></v-divider>

            <v-list-item v-for="item in read" :key="item.id">
                <v-list-item-title>{{item.question}}</v-list-item-title>
            </v-list-item>
        </v-list>
        </v-menu>
    </div>

</template>

<script>
export default {
  data() {
    return {
      read: {},
      unread: {},
      unreadCount: 0,
    //   sound: "http://soundbible.com/mp3/glass_ping-Go445-1207030150.mp3"
    };
  },
  created() {
    if (User.loggedIn()) {
      this.getNotifications();
    }
    Echo.private("App.User." + User.id())
    .notification((notification) => {
    //   this.playSound();
      this.unread.unshift(notification);
      this.unreadCount++;
    });
  },
  methods: {
    // playSound() {
    //   let alert = new Audio(this.sound);
    //   alert.play();
    // },
    getNotifications() {
      axios
        .post("/api/notifications")
        .then(res => {
          this.read = res.data.read;
          this.unread = res.data.unread;
          this.unreadCount = res.data.unread.length;
        })
        .catch(error => Exception.handle(error));
    },
    readIt(notification) {
      axios.post("/api/markAsRead", { id: notification.id }).then(res => {
        this.unread.splice(notification, 1);
        this.read.push(notification);
        this.unreadCount--;
      });
    }
  },
  computed: {
    color() {
      return this.unreadCount > 0 ? "orange" : "orange lighten-4";
    }
  }
};
</script>

<style>

</style>
