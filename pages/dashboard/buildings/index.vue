<template>
	<div> 
		<v-row>
			<v-col class="col-md-4 offset-md-8">
				<v-btn @click.prevent="fetchPrivateBuildings" :color="private ? 'green' : ''">
					Mes immeubles
				</v-btn>
				<span>/</span>
				<v-btn @click.prevent="fetchBuildings" :color="private ? '' : 'green'">
					Tous
				</v-btn>
			</v-col>
			
			<building-card v-for="building in buildings.data" :building="building" :key="building.id" class="mt-16" />
		</v-row>
	</div>
</template>

<script>
	import buildingCard from '@/components/building/buildingCard'
	export default {
		layout : 'dashboard',
		head() {
			return {
				title : 'Buildings'
			}
		},
		components : ['buildingCard'],
		data () {
			return {
				buildings : null,
				private : true
			}
		},
		methods : {
			async fetchBuildings() {
				this.buildings = await this.$axios.$get('buildings')
				this.private = false
			},
			async fetchPrivateBuildings() {
				this.buildings = await this.$axios.$get('me/buildings')
				this.private = true
			}
		},

		async asyncData({app}) {
			let buildings = await app.$axios.$get('me/buildings')
			return { buildings : buildings }
		}
	}
</script>