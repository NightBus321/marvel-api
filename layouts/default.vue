<template>   
  <v-app dark>
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-toolbar-title>{{ title }}</v-toolbar-title>
      <v-spacer />
      <v-menu offset-y>
        <v-list>
          <v-list-item to="/profile">
            <v-list-item-title></v-list-item-title>
          </v-list-item>
          <v-list-item @click="closeSesion">
            <v-list-item-title>Salir</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default { 
  name: 'DefaultLayout',
  beforeMount() {
    this.loadAccount()
  },
  data() {
    return { 
      message: 'Marvel-api',
      fullname: "",
      clipped: true,
      fixed: false,
      miniVariant: false,
      title: 'MARVEL CHARACTERS',
    }
  }, 
  mounted(){
    window.document.title = this.message; 
  }, 
  methods: {
    closeSesion() {
      this.$router.push("/")
    },
    loadAccount() {
      const account_str = localStorage.getItem("ACCOUNT")
      if (account_str) {
        try {
          const account = JSON.parse(account_str)
          this.fullname = `${account.firstname} ${account.lastname}`
          //TODO: Validando el rol pendiente desde el API
          if (account.role == 0) {
            this.$router.push("/students/home")
          } else {
            this.$router.push("/home")
          }
        } catch (error) {
          this.$router.push("/")
        }
      } else {
        this.$router.push("/")
      }
    }
  }
}
</script>
