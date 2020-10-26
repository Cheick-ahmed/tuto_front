<template>
	<div>
		<v-snackbar v-model="notification.snackbar">
			{{ notification.text }}
		</v-snackbar>

		<div>
			<v-row>
				<v-col sm="8" lg="6">
					<h1>Informations personnelles</h1>
					<v-card>
						<v-card-text class="mt-4">
							<v-form @submit.prevent="updateProfile" lazy-validation>
								<v-text-field v-model="form.name" label="Votre nom complet" :error-messages="validation.name" required></v-text-field>

								<v-text-field class="mt-3" v-model="form.email" label="Votre email" type="email" :error-messages="validation.email" required></v-text-field>

								<v-btn :disabled="validation.errors" type="submit" color="primary" class="mt-4">
									Enregistrer
								</v-btn>
							</v-form>
						</v-card-text>
					</v-card>
				</v-col>

				<v-col sm="8" lg="6">
					<h1>Mot de passe</h1>
					<v-card>
						<v-card-text class="mt-4">
							<v-form @submit.prevent="updatePassword" lazy-validation>

								<v-text-field v-model="form.current_password" label="Mot de passe actuel" type="password" :error-messages="validation.current_password" required></v-text-field>

								<v-text-field class="mt-3" v-model="form.password" label="Nouveau mot de passe" type="password" :error-messages="validation.password" required></v-text-field>

								<v-text-field class="mt-3" v-model="form.password_confirmation" label="Confirmez le nouveau mot de passe" type="password" required></v-text-field>

								<v-btn :disabled="validation.errors" type="submit" color="primary" class="mt-4">
									Modifier
								</v-btn>
							</v-form>
						</v-card-text>
					</v-card>
				</v-col>
			</v-row>
		</div>
	</div>
</template>

<script>
export default {
	layout : 'dashboard',
	head() {
		return {
			title : 'Mon compte'
		}
	},
	data () {
		return {
			validation : {},
			notification : {
				snackbar : false,
				text : ''
			},
			form : {
				name : this.$auth.user[0].name,
				email : this.$auth.user[0].email,
				current_password : '',
				password : '',
				password_confirmation : ''
			}
		}
	},
	methods : {
		async updateProfile () {
			try {
				await this.$axios.patch('account/profile', {
					name : this.form.name,
					email : this.form.email
				})
				await this.$auth.fetchUser()

				setTimeout(() => {
					this.notification.for = 'profile'
					this.notification.snackbar = true,
					this.notification.text = 'Vos informations ont bien été mise à jour.'
				},500)

			} catch (e) {
				console.log(e.response.data.errors)
				this.validation = e.response.data.errors
			}
		},

		async updatePassword () {
			try {
				await this.$axios.patch('account/password', {
					current_password : this.form.current_password,
					password : this.form.password,
					password_confirmation : this.form.password_confirmation
				})
				await this.$auth.fetchUser()
				setTimeout(() => {
					this.notification.for = 'profile'
					this.notification.snackbar = true,
					this.notification.text = 'Votre mot de passe a bien été mis à jour.'
				},500)
			} catch (e) {
				console.log(e)
				this.validation = e.response.data.errors
			}
			
		}
	}
}
</script>