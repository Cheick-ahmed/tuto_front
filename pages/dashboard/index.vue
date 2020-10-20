<template>
	<div>
		<h1>Mon compte</h1>
		<v-row class="mt-8">
			<v-col sm="8" lg="6">
				<v-card>
					<v-card-title>
						Mes informations personnelles
					</v-card-title>
					<v-card-text class="mt-4">
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
						color="primary"
						class="mt-4"
						>
						Enregistrer
					</v-btn>
				</v-form>
			</v-card-text>
		</v-card>
	</v-col>
</v-row>
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
			form : {
				name : 'Cheick Ahmed Sidibé',
				email : 'chs.ahmed_pro02@outlook.com',
				password : 'ahmedahmed',
				password_confirmation : 'ahmed_ahmed'
			}
		}
	},
	methods : {
		submit () {
			console.log('Profile updated.')
		}
	}
}
</script>