<template>
  <div class="pt-16">
    <v-row align="center" justify="center">
      <v-col sm="6" lg="8" xl="4" class="mt-16">
        <v-form
        ref="form"
        @submit.prevent="submit"
        lazy-validation
        >
        <v-text-field
        v-model="form.name"
        label="Votre nom complet"
        required
        ></v-text-field>


        <v-text-field
        v-model="form.email"
        label="Votre email"
        type="email"
        required
        ></v-text-field>

        <v-text-field
        v-model="form.password"
        label="Choisissez un mot de passe"
        type="password"
        required
        ></v-text-field>

        <v-text-field
        v-model="form.password_confirmation"
        label="Confirmez votre mot de passe"
        type="password"
        required
        ></v-text-field>

        <v-btn
        :disabled="validation.errors"
        type="submit"
        color="blue lighten-1"
        class="mt-4"
        >
        Inscription
      </v-btn>

    </v-form>
  </v-col>
</v-row>
</div>

</template>

<script>
export default {
  head() {
    return {
      title : 'Inscription'
    }
  },
  data() {
    return {
      validation : {},
      form : {
        name : '',
        email : '',
        password : '',
        password_confirmation : ''
      }
    }
  },

  methods: {
    validate () {
      this.$refs.form.validate()
    },
    submit() {
      console.log(this.form)
    }
  },
}
</script>
