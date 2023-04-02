<template>
  <div>
    <h1>LOAD MARVEL CHARACTERS</h1>
    <v-btn @click="loadAccounts" :disabled="loading">Cargar cuentas</v-btn>
    <br />
    <span v-if="loading">Cargando...</span>
    <v-progress-linear
      v-if="loading"
      indeterminate
      color="cyan"
    ></v-progress-linear>
    <br />
    <div>
      <ul style="list-style: none; display: flex; flex-wrap: wrap; margin: 0; padding: 0;">
        <li v-for="account in accounts" :key="account.id" style="width: 32%; box-sizing: border-box; text-align: center; margin: 5px;">
          <v-card class="mx-auto" max-width="344">
            <v-img
              :src="account.thumbnail.path + '.' + account.thumbnail.extension"
              height="200px"
              cover
            ></v-img>

            <v-card-title> {{ account.name }}</v-card-title>

            <v-card-subtitle>{{ account.description }}</v-card-subtitle>

            <v-card-actions>
              <v-spacer></v-spacer>

              <v-btn @click="show = !show">Learn more</v-btn>
            </v-card-actions>

            <v-expand-transition>
              <div v-show="show">
                <v-divider></v-divider>

                <v-card-text>
                  Cantidad de comics: {{ account.comics.available }}
                  <br />
                  Cantidad de series: {{ account.series.available }}
                  <br />
                  Cantidad de stories: {{ account.stories.available }}
                  <br />
                  Cantidad de eventos: {{ account.events.available }}
                  <br />
                  <ul>
                    <li
                      v-for="serie in account.series.items.slice(0, 3)"
                      :key="serie.name"
                    >
                      {{ serie.name }}
                    </li> 
                  </ul> 
                </v-card-text>
              </div>
            </v-expand-transition>
          </v-card> 
          <br>
        </li> 
      </ul> 
    </div>
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