<template>
  <div>
    <h1>LOAD MARVEL CHARACTERS</h1>
    
  </div>
</template>

<script lang="ts">
export default {
  data() {
    return {
      accounts: [],
      loading: false, 
      show: false
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