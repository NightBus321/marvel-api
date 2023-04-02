<template>
  <div>
    <h1>LOAD MARVEL CHARACTERS</h1>
    <v-card class="mx-auto" max-width="344">
      <v-img
        src="https://cdn.vuetifyjs.com/images/cards/sunshine.jpg"
        height="200px"
        cover
      ></v-img>

      <v-card-title> Top western road trips </v-card-title>

      <v-card-subtitle> 1,000 miles of wonder </v-card-subtitle>

      <v-card-actions>
        <v-btn color="orange-lighten-2" variant="text"> Explore </v-btn>

        <v-spacer></v-spacer>

        <v-btn
          :icon="show ? 'mdi-chevron-up' : 'mdi-chevron-down'"
          @click="show = !show"
        ></v-btn>
      </v-card-actions>

      <v-expand-transition>
        <div v-show="show">
          <v-divider></v-divider>

          <v-card-text>
            I'm a thing. But, like most politicians, he promised more than he
            could deliver. You won't have time for sleeping, soldier, not with
            all the bed making you'll be doing. Then we'll go with that data
            file! Hey, you add a one and two zeros to that or we walk! You're
            going to do his laundry? I've got to find a way to escape.
          </v-card-text>
        </div>
      </v-expand-transition>
    </v-card>
  </div>
</template>

<script lang="ts">
export default {
  data() {
    return {
      accounts: [],
      loading: false,
      show: false,
    }
  },
  methods: {
    loadAccounts() {
      console.log('Cargar cuentas')
      const url =
        'https://gateway.marvel.com:443/v1/public/characters?ts=10&apikey=af468b3503603801817dfff31982be6b&hash=70f8e7fd7ba77a7d1ad086d52bc20bc6'
      this.loading = true
      this.$axios
        .get(url)
        .then((response) => {
          const data = response.data
          this.accounts = data.data.results
          console.log(response)
        })
        .catch((error) => {
          alert('Ha ocurrido un error al cargar los personajes')
          console.log(error)
        })
        .finally(() => {
          this.loading = false
        })
    },
  },
}
</script>

<style></style>