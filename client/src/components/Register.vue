<template>
  <div>
    <v-container padding fluid>
      <v-row align="center" justify="center">
        <v-col cols="12" sm="8" md="4">
          <v-card class="elevation-12">
            <v-toolbar
              color="primary"
              dark
              flat>
              <v-toolbar-title>
                Register
              </v-toolbar-title>
              <v-spacer />
            </v-toolbar>
            <v-card-text>
              <v-form name="cena-rap-form">
                <v-text-field
                  prepend-icon="email"
                  label="Email"
                  v-model="email"
                ></v-text-field>
                <br>
                <v-text-field
                  prepend-icon="lock"
                  label="Password"
                  type="password"
                  v-model="password"
                  autocomplete="new-password"
                ></v-text-field>
                <br>
                <div class="danger-alert" v-html="error" />
                <br>
              </v-form>
            </v-card-text>
            <v-card-actions>
              <v-spacer />
              <v-btn
                class="v-btn v-btn--rounded v-btn--loading theme--light elevation-0 v-size--large accent-4"
                dark
                @click="register">
                Register
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
export default {
  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },
  methods: {
    async register () {
      try {
        const response = await AuthenticationService.register({
          email: this.email,
          password: this.password
        })
        this.$store.dispatch('setToken', response.data.token)
        this.$store.dispatch('setUser', response.data.user)
        this.$router.push({
          name: 'songs'
        })
      } catch (error) {
        this.error = error.response.data.error
      }
    }
  }
}
</script>
<style scoped>
.container.fluid{
  max-width: 50%;
}
.home {
  cursor: pointer;
}
.home:hover {
  color: red;
}
.padding {
  padding-top: 200px;
  padding-right: 50px;
  padding-bottom: 0px;
  padding-left: 50px;
}
</style>