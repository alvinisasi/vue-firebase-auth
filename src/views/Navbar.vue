<template>
  <v-toolbar>
    <v-toolbar-side-icon></v-toolbar-side-icon>
    <v-toolbar-title>Title</v-toolbar-title>
    <v-spacer></v-spacer>
    <v-toolbar-items class="hidden-sm-and-down">
      <v-btn flat v-for="item in items" :key="item.title" to="item.link">
          <v-icon right>{{item.icon}}</v-icon>{{item.title}}
      </v-btn>
    </v-toolbar-items>
    <v-toolbar-items class='hidden-xs-only'>
        <v-btn
            flat
            >
            <v-icon right>delete_sweep</v-icon>Logout
        </v-btn>
    </v-toolbar-items>
  </v-toolbar>
</template>

<script>
export default {
    computed: {
    items() {
        let menuItems = [
            {
                title: 'Register',
                icon: 'face',
                link: '/register'
            },
            {
                title: 'Login',
                icon: 'no_encryption',
                link: '/login'
            }
        ]
        return menuItems
    }
}
}
</script>