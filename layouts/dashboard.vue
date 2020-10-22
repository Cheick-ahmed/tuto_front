<template>
	<v-app>
		<v-app-bar app>
			<v-spacer></v-spacer>
			<v-btn text class="mr-4">
				Account
			</v-btn>
			<v-btn text>
				Buildings
			</v-btn>

			<v-btn text class="ml-6" @click.prevent="logout">
				Logout
			</v-btn>
		</v-app-bar>
		<v-main>
			<v-container class="pt-16">
				<nuxt />
			</v-container>
		</v-main>
	</v-app>
</template>

<script>
	export default {
		middleware : 'auth',
		methods : {
			logout () {
				this.$auth.logout()
			}
		}
	}
</script>