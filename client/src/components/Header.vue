<template>
  <v-toolbar fixed class="black" dark>
    <v-toolbar-title class="mr-4">
      <router-link 
        class="home"
        tag="span"
        :to="{
          name: 'songs'
        }">
        Cena RAP
      </router-link>
    </v-toolbar-title>

    <v-spacer></v-spacer>

    <v-toolbar-items>
      <v-btn 
        v-if="!$store.state.isUserLoggedIn"
        dark
        v-text="'Login'"
        :to="{
          name: 'login'
        }"/>
      
      <v-btn 
        v-if="!$store.state.isUserLoggedIn"
        v-text="'Sign Up'"  
        dark
        :to="{
          name: 'register'
        }"/>
      
      <v-btn 
        v-if="$store.state.isUserLoggedIn"
        v-text="'Log Out'" 
        dark
        @click="logout"
        />
    </v-toolbar-items>
  </v-toolbar>
</template>

<script>
export default {
  methods: {
    logout () {
      this.$store.dispatch('setToken', null)
      this.$store.dispatch('setUser', null)
      this.$router.push({
        name: 'songs'
      })
    }
  }
}
</script>

<style scoped>
.home {
  cursor: pointer;
}
.home:hover {
  color: red;
}
</style>