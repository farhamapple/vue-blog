<template>
  <v-app>
    
    <alert/>

    <v-navigation-drawer app v-model="drawer">
      <!-- -->
      <v-list>
        <v-list-item v-if="!guest">
            <v-list-item-avatar>
              <v-img src="https://randomuser.me/api/portrails/men/78.jpg"></v-img>
            </v-list-item-avatar>
            <v-list-item-content>
              <v-list-item-title>Farham Harvianto</v-list-item-title>
            </v-list-item-content>
        </v-list-item>

        <div class="pa-2" v-if="guest">
          <v-btn block color="primary" class="mb-1" @click="login">
            <v-icon left>mdi-lock</v-icon>
            Login
          </v-btn>
          <v-btn block color="success">
            <v-icon left>mdi-account</v-icon>
            Register
          </v-btn>
        </div>
        <v-divider></v-divider>
        <v-list-item 
        v-for="(item, index) in menus" 
        :key="`menu-${index}`" 
        :to="item.route">
          <v-list-item-icon>
            <v-icon left>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>

      <template v-slot:append v-if="!guest">
        <div class="pa-2">
          <v-btn block color="red" dark @click="logout">
            <v-icon left>
              mdi-lock
            </v-icon>
            Logout
          </v-btn>
        </div>
      </template>
      
    </v-navigation-drawer>

    <v-app-bar app color="success" dark>
      <!-- -->
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>SanberCoe App</v-toolbar-title>
      <v-spacer></v-spacer>
    </v-app-bar>

    <!-- Sizes your content based upon application components -->
    <v-main>

      <!-- Provides the application the proper gutter -->
      <v-container fluid>

        <!-- If using vue-router -->
        <v-slide-y-transition>
          <router-view></router-view>
        </v-slide-y-transition>
      </v-container>
    </v-main>

    <v-footer app>
      <!-- -->
      @SanberCode | Vue JS
    </v-footer>
  </v-app>
</template>

<script>
import { mapActions } from 'vuex'
//import Alert from './components/Alert.vue';

export default {
  components: { 
    Alert : () => import('./components/Alert.vue')
  },
  name: 'App',

  data: () => ({
    drawer : false,
    menus : [
      {
        title: 'Home',
        icon : 'mdi-home',
        route : '/'
      },
      {
        title: 'Blogs',
        icon : 'mdi-note',
        route : '/blogs'
      },
    ],
    guest : true,
    //snackbarStatus: false,
    //snackbarText: 'Anda Berhasil Login'
  }),
  mounted(){
    //this.snackbarStatus = true
  },
  methods : {
    logout(){
      this.guest = true,
      this.setAlert({
        status: true,
        color : 'success',
        text : 'Anda Berhasil Logout'
      })
    },

    login(){
      this.guest = false,
      this.setAlert({
        status: true,
        color : 'success',
        text : 'Anda Berhasil Logout'
      })
    },

    ...mapActions({
      setAlert : 'alert/set'
    })
    

  }

};
</script>
