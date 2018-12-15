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
					<listViewItem @mouseover.native="clickQuickView(index)" v-for="(truck, index) in trucks" :title="truck.title" :desc="truck.description" />
				</div>
				<div v-else>
					Map View
				</div>

			</div>
			<div class="quickView">

				<quickView :title="trucks[quickViewActive].title" />

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
				{title: 'Title 0', description: 'Something goes here.'},
				{title: 'Title 1', description: 'Something goes here.'},
				{title: 'Title 2', description: 'Something goes here.'},
				{title: 'Title 3', description: 'Something goes here.'},
				{title: 'Title 4', description: 'Something goes here.'},
				{title: 'Title 5', description: 'Something goes here.'},
				{title: 'Title 6', description: 'Something goes here.'},
				{title: 'Title 7', description: 'Something goes here.'},
				{title: 'Title 8', description: 'Something goes here.'}
			], 
			quickViewActive: 0
		}
	},
	methods: {
		listViewClick() {
			this.listView = 1;
		},
		mapViewClick() {
			this.listView = 0;
		},
		clickQuickView(e) {
			this.quickViewActive = e;
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