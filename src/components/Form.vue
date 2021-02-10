<template>
  <v-container>    
    <v-form ref="form" v-model="valid" lazy-validation>
      <v-row>
        <v-col cols="12" sm="12" md="6">
          <v-text-field
            v-model="dataForm.title"            
            :rules="titleRules"
            label="Title"
            required>
          </v-text-field>
        </v-col>

        <v-col cols="12" sm="12" md="6">
          <v-text-field
            v-model="dataForm.description"
            :counter="40"
            :rules="descriptionRules"
            label="Description"
            required>
          </v-text-field>
        </v-col>
      </v-row>

      <v-row>
        <v-col cols="12" sm="12" md="6">
          <v-autocomplete
            v-model="dataForm.severity"
            :items="severityItems"
            :rules="[v => !!v || 'Severity is required']"
            label="Severity"
            item-value="id"
            item-text="level"
            required>
          </v-autocomplete>
        </v-col>

        <v-col cols="12" sm="12" md="6">
          <v-autocomplete
            v-model="dataForm.state"
            class="status"
            :items="statusItems"
            :rules="[v => !!v || 'State is required']"
            label="State"
            item-value="id"
            item-text="state"
            required>
          </v-autocomplete>
        </v-col>
      </v-row>

      <v-row>        
        <v-col cols="12" sm="12" md="6">
          <v-autocomplete
            v-model="dataForm.user"
            :items="users"
            :rules="[v => !!v || 'User is required']"
            label="User"
            persistent-hint
            item-value="id"
            item-text="name"
            prepend-icon="mdi-account-circle">
          </v-autocomplete>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12" sm="3" md="2">
          <v-btn :disabled="!valid" color="success" class="mr-2" @click="validate">
            Validate
          </v-btn>
        </v-col>
        <v-col cols="12" sm="3" md="2">
          <v-btn color="error" class="mr-2" @click="reset">
            Reset Form
          </v-btn>
        </v-col>
        <v-col cols="12" sm="3" md="1">
          <v-btn color="warning" @click="resetValidation">
            Reset Validation
          </v-btn>
        </v-col>
      </v-row>
    </v-form>
  </v-container>
</template>
<script>
const axios = require('axios')

export default {
  name: 'Formulario',
  watch: {
    dataForm: {
      handler () {
        this.saveForm()
      },
      deep: true
    }
  },
  data: () => ({
    users: [],
    dataForm: {},
    valid: true,
    title: '',
    titleRules: [
      v => !!v || 'Title is required'
    ],
    description: '',
    descriptionRules: [
      v => !!v || 'Decription is required',
      v => (v && v.length <= 40) || 'Description must be less than 40 characters',
      v => (v && v.length >= 10) || 'Description must be greater than 10 characters'
    ],
    severityItems: [
      { id: 1, level: 'High' },
      { id: 2, level: 'Medium' },
      { id: 3, level: 'Low' }
    ],
    statusItems: [
      { id: 1, state: 'TODO' },
      { id: 2, state: 'DOING' },
      { id: 3, state: 'DONE' }
    ]
  }),
  created () {
    this.getUsers()
  },
  methods: {
    saveForm () {
      localStorage.setItem('dataForm', JSON.stringify(this.dataForm))
      console.log('Se han modificado datos del formulario: ', this.dataForm)
    },
    validate () {
      this.$refs.form.validate()
    },
    reset () {
      this.$refs.form.reset()
    },
    resetValidation () {
      this.$refs.form.resetValidation()
    },
    getUsers () {
      axios.get('https://jsonplaceholder.typicode.com/users').then(response => {
          // handle success
          console.log(response.data)
          this.users = response.data
        })
        .catch(error => {
          // handle error
          console.log(error)
        })
    }
  }
}
</script>