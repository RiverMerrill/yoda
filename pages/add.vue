<template>
  <v-form v-model="valid">
    <v-container>
      <nuxt-link to="/">
        <v-btn
          fab
          outline
          small
          absolute
          left
          color="primary"
        >
          <v-icon dark>
            keyboard_arrow_left
          </v-icon>
        </v-btn>
      </nuxt-link>
      <h1 class="text-xs-center">Enter some info about your yoda session.</h1>
      <v-layout
        row
        wrap
        mx-auto
      >
        <v-flex xs12>
          <v-text-field
            v-model="firstName"
            :rules="nameRules"
            label="First name"
            required
          ></v-text-field>
        </v-flex>

        <v-flex xs12>
          <v-text-field
            v-model="lastName"
            :rules="nameRules"
            label="Last name"
            required
          ></v-text-field>
        </v-flex>

        <v-flex xs12>
          <v-text-field
            v-model="email"
            :rules="emailRules"
            label="E-mail"
            required
          ></v-text-field>
        </v-flex>
        <v-flex xs12>
          <v-text-field
            v-model="topic"
            label="Topic"
            required
          ></v-text-field>
        </v-flex>

        <v-btn
          class="elevation-12"
          color="primary"
          large
        >
          submit
        </v-btn>
      </v-layout>
    </v-container>
  </v-form>
</template>

<style>
</style>

<script>
export default {
  data: () => ({
    valid: false,
    firstName: '',
    lastName: '',
    email: '',
    topic: '',
    nameRules: [
      v => !!v || 'Name is required',
      v => v.length <= 10 || 'Name must be less than 10 characters'
    ],
    emailRules: [
      v => !!v || 'E-mail is required',
      v => /.+@.+/.test(v) || 'E-mail must be valid'
    ]
  })
}
</script>

