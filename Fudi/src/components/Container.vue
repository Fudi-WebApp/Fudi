<template>
	<section>
		<div class="wrap">
			<div class="list">
				
				<div class="options">
					<div @click="listViewClick" class="btn">
						<span>List View</span>
					</div>
					<div @click="mapViewClick" class="btn">
						<span>Map View</span>
					</div>
					<span class="activeTrucks">{{activeTrucks}} Active Trucks</span>
				</div>

				<div v-if="listView == 1">
					<listViewItem v-for="truck in trucks" :title="truck.title" :desc="truck.description" />
				</div>
				<div v-else>
					Map View
				</div>

			</div>
			<div class="quickView">

				<quickView />

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
			activeTrucks: 0,
			listView: 1,
			trucks: [
				{title: 'Title', description: 'Something goes here.'},
				{title: 'Title', description: 'Something goes here.'},
				{title: 'Title', description: 'Something goes here.'},
				{title: 'Title', description: 'Something goes here.'},
				{title: 'Title', description: 'Something goes here.'},
				{title: 'Title', description: 'Something goes here.'},
				{title: 'Title', description: 'Something goes here.'},
				{title: 'Title', description: 'Something goes here.'},
				{title: 'Title', description: 'Something goes here.'}
			]
		}
	},
	methods: {
		listViewClick() {
			this.listView = 1;
		},
		mapViewClick() {
			this.listView = 0;
		}
	},
	created() {
		this.activeTrucks = this.trucks.length;
	},
	components: {
		listViewItem,
		quickView
	}
}
</script>

<style scoped>

</style>