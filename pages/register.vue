<template>
  <div class="pt-16">
    <v-row align="center" justify="center">
      <v-col sm="6" lg="8" xl="4" class="mt-16">
        <v-form @submit.prevent="submit">
          <v-text-field v-model="form.name" label="Votre nom complet" :error-messages="validation.name" required></v-text-field>

          <v-text-field v-model="form.email" label="Votre email" type="email" :error-messages="validation.email" required></v-text-field>

          <v-text-field v-model="form.password" label="Choisissez un mot de passe" type="password" :error-messages="validation.password" required></v-text-field>

          <v-text-field v-model="form.password_confirmation" label="Confirmez votre mot de passe" type="password" required></v-text-field>

          <v-btn :disabled="validation.errors" type="submit" color="blue lighten-1"class="mt-4">
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
    async submit() {
      try {
        await this.$axios.post('auth/register', this.form )

        await this.$auth.loginWith('local',{
          data : {
            email : this.form.email,
            password : this.form.password
          }
        })

        this.$router.push({
          name : 'dashboard'
        })
        
      } catch (e) {
        this.validation = e.response.data.errors
      }

    }
  },
}
</script>
