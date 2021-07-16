<template>
  <nav>
    
    <v-app-bar color="deep-purple" dark>
        <v-app-bar-nav-icon @click="drawer = true"></v-app-bar-nav-icon>

        <v-toolbar-title class="pl-0">
            <span class="font-weight-light">High</span>
            <span>Python</span>
        </v-toolbar-title>
        <v-spacer></v-spacer>
        
        <v-btn depressed small>
            <v-icon>code</v-icon>
            <span>github</span>
        </v-btn>

        <v-navigation-drawer v-model="drawer" app>
            <p>test</p>
        </v-navigation-drawer>
    </v-app-bar>

    <v-navigation-drawer v-model="drawer" absolute temporary>
      <v-list nav dense >
        <v-list-item-group
          v-model="group"
          active-class="deep-purple--text text--accent-4"
        >
          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-home</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Home</v-list-item-title>
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
            drawer: false
        }
    }

}
</script>
