<template>
	<v-app>
		<v-app-bar app>
			<v-spacer></v-spacer>
			<v-btn flat class="mr-4">
				Mon compte
			</v-btn>
			<v-btn flat>
				Immeubles
			</v-btn>
		</v-app-bar>
		<v-main>
			<v-container class="pt-16">
				<nuxt />
			</v-container>
		</v-main>
	</v-app>
</template>