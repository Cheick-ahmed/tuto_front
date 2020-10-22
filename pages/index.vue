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
        v-model="form.email"
        label="Votre email"
        type="email"
        :error-messages="validation.email"
        required
        ></v-text-field>

        <v-text-field
        class="mt-4"
        v-model="form.password"
        label="Votre mot de passe"
        type="password"
        :error-messages="validation.password"
        required
        ></v-text-field>

        <v-btn
        :disabled="validation.errors"
        type="submit"
        :color="validation.email || validation.password ? 'error' : 'primary'"
        class="mt-6"
        >
        Connexion
      </v-btn>

    </v-form>
  </v-col>
</v-row>
</div>

</template>

<script>
export default {
  head () {
    return {
      title : 'Connexion à votre compte'
    }
  },
  data() {
    return {
      validation : {},
      form : {
        email : 'chs.ahmed_pro02@outlook.com',
        password : 'ilovecats'
      }
    }
  },

  methods: {
    async submit() {
      try {
        await this.$auth.loginWith('local', {
          data : this.form
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
