<template>
  <nav>
    
    <v-app-bar color="teal " dark>
        <v-app-bar-nav-icon @click="drawer = true"></v-app-bar-nav-icon>

        <v-toolbar-title class="pl-0">
            <span class="font-weight-light">High</span>
            <span>Python</span>
        </v-toolbar-title>
        <v-spacer></v-spacer>
        
        <a href="https://github.com/osamamhd/high-python-vue">
        <v-btn depressed small class="d-none d-sm-flex" color="cyan darken-3">
            <i class="fab fa-github"></i>
            <span>github</span>
        </v-btn>
        </a>
        <v-navigation-drawer v-model="drawer" app>
            <p>test</p>
        </v-navigation-drawer>
    </v-app-bar>

    <v-navigation-drawer v-model="drawer" absolute temporary>
      <v-layout column align-center>
        <v-flex class="mt-5">
          <v-avatar size="100">
            <img src="/logo.png" alt="">
          </v-avatar>
          <h3 class="subhearding mt-1 teal--text">High Python</h3>
        </v-flex>
      </v-layout>
      <v-list nav dense >
        <v-list-item-group active-class="teal--text text--accent-4">
          <v-list-item v-for="link in links" :key="link.text" router :to="link.route">
            <v-list-item-icon>
              <v-icon>{{ link.icon }}</v-icon>
            </v-list-item-icon>
            <v-list-item-title>{{ link.text }}</v-list-item-title>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>
      
  </nav>
</template>

<script>
export default {
    data() {
        return {
            drawer: false,
            links: [
              { icon: 'home', text: 'Home', route:'/'},
              { icon: 'category', text: 'Categories', route:'/categories'},
              { icon: 'info', text: 'About', route:'/about'}
            ]
        }
    }

}
</script>
