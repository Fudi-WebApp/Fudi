<template>
	<section>
		<div class="wrap">
			<div class="list">
				<div class="options">
					<div class="btn">
						<span>List View</span>
					</div>
					<div class="btn">
						<span>Map View</span>
					</div>
					<span class="activeTrucks">{{activeTrucks}} Active Trucks</span>
				</div>
				
				<listViewItem v-for="truck in trucks" :title="truck.title" :desc="truck.description" />
				
			</div>
			<div class="quickView">

				<quickView/>

			</div>
		</div>
	</section>
</template>

<script>
import listViewItem from './ListViewItem'
import quickView from './QuickView'

export default {
	name: 'Container',

	data () {
		return {
			activeTrucks: 31,
			trucks: [
				{title: 'Title', description: 'Something goes here.'},
				{title: 'Title', description: 'Something goes here.'},
				{title: 'Title', description: 'Something goes here.'}
			]
		}
	},
	components: {
		listViewItem,
		quickView
	}
}
</script>

<style scoped>

</style>