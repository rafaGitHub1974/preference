<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <v-img alt="Vuetify Logo" class="shrink mr-2" contain src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png" transition="scale-transition" width="40"/>
      </div>

      <v-spacer></v-spacer>

      <v-btn href="http://www.prefsuite.com/spain/new/" target="_blank" text>
        <span class="mr-2">Prueba Preference</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <Form />
    </v-main>
  </v-app>
</template>

<script>
import Form from './components/Form'

export default {
  name: 'App',

  components: {
    Form
  },

  data: () => ({
  })
}
</script>
