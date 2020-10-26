<template>
	<v-col sm="8" lg="6" >
		<v-card>
			<v-card-title>
				<v-icon large left>
					mdi-office-building
				</v-icon>
				<span class="title font-weight-light">{{ building.title }}</span>
			</v-card-title>
			<v-card-text class="headline font-weight-bold">
				{{ building.description }}
			</v-card-text>
		</v-card>
	</v-col>
</template>
<script>
export default {
	props : {
		building : {
			required : true,
			type : Object
		}
	}
}
</script>