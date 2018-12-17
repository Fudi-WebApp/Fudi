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
					<!-- <div @click="favoritesViewClick" class="btn">
						<span>Favorites</span>
					</div> -->
					<div @click="prevPage" v-if="activePage > 1" class="btn">
						<span>Prev</span>
					</div>
					<div @click="nextPage" v-if="activePage < totalPages" class="btn">
						<span>Next</span>
					</div>
					Page: {{activePage}} | {{totalPages}}
					<span v-if="listView == 0 || listView == 1" class="activeTrucks">{{activeTrucks}} Active<br>Showing {{totalOnPage}}</span>
					<span v-else class="activeTrucks">{{favoriteTrucks}} Favorite Trucks</span>
				</div>

				<div v-if="listView == 0">
					<!-- <listViewItem @mouseover.native="hoverQuickView(index)" v-for="(truck, index) in trucks" :title="truck.title" :desc="truck.description" :tags="truck.tags" :distance="truck.distance" :favorite="truck.favorite" :image="truck.image" /> -->
					<div class="loading" v-if="loading == 1"><p>Loading...</p></div>
					<listViewItem @mouseover.native="hoverQuickView(index)" v-for="(truck, index) in wordpress[wordpress.length - 1]" :title="truck.title.rendered" :desc="truck.content.rendered" :slug="truck.slug" :excerpt="truck.excerpt.rendered" :tags="truck.meta" :distance="truck.id" :favorite="truck.id" :image="truck.id" />
				</div>
				<div v-else-if="listView == 1">
					Map View
				</div>
				<div v-else-if="listView == 2">
					<listViewItem @mouseover.native="hoverQuickView(index)" v-for="(truck, index) in trucks" v-if="truck.favorite != 0" :title="truck.title" :desc="truck.description" :tags="truck.tags" :distance="truck.distance" :favorite="truck.favorite" :image="truck.image" />
				</div>

			</div>
			<div class="quickView">

				<!-- <quickView v-if="quickViewActive != null" :title="trucks[quickViewActive].title" :facebook="trucks[quickViewActive].facebook" :twitter="trucks[quickViewActive].twitter" :website="trucks[quickViewActive].website" :phone="trucks[quickViewActive].phone" :tags="trucks[quickViewActive].tags" :image="trucks[quickViewActive].image" /> -->
				<quickView v-if="quickViewActive != null" :title="wordpress[wordpress.length - 1][quickViewActive].title.rendered" :slug="wordpress[wordpress.length - 1][quickViewActive].slug" :facebook="wordpress[wordpress.length - 1][quickViewActive].id" :twitter="wordpress[wordpress.length - 1][quickViewActive].id" :website="wordpress[wordpress.length - 1][quickViewActive].id" :phone="wordpress[wordpress.length - 1][quickViewActive].id" :tags="wordpress[wordpress.length - 1][quickViewActive].meta" :image="wordpress[wordpress.length - 1][quickViewActive].id" />

			</div>
		</div>
	</section>
</template>

<script>
import listViewItem from './ListViewItem'
import quickView from './QuickView'

import axios from 'axios'

export default {
	name: 'Container',
	data () {
		return {
			activeTrucks: 0,
			favoriteTrucks: 0,
			listView: 0,
			trucks: [], 
			quickViewActive: null, 
			wordpress: [],
			loading: 1,
			headers: [],
			totalPages: 1,
			activePage: 1,
			totalOnPage: 0, 
			perPage: 20
		}
	},
	methods: {
		listViewClick() {
			this.listView = 0;
		},
		mapViewClick() {
			this.listView = 1;
		},
		favoritesViewClick() {
			this.listView = 2;
		},
		hoverQuickView(e) {
			this.quickViewActive = e;
		},
		updateList() {
			this.trucks.push(
				{	
					title: 'Really Long Title That I Want To Make Really Long Just To See How A Long Title Works', 
					description: 'Something cool about this food truck that isn’t too long, gets the point across and helps explain what kind of food this truck is cookin up.',
					facebook:'facebook.com',
					twitter:'twitter.com',
					website:'google.com',
					phone:'555-555-5555',
					tags: ['Stuff', 'Food', 'Excellent'],
					distance: 1.2,
					favorite: 1,
					image: 'http://www.kindredpdx.com/wp-content/uploads/2013/08/CART-ROW-BW-LOGO.jpg'
				},
				{	
					title: 'Title 1', 
					description: 'Something cool about this food truck that isn’t too long, gets the point across and helps explain what kind of food this truck is cookin up.',
					facebook:'facebook.com',
					twitter:'twitter.com',
					website:'google.com',
					phone:'555-555-5555',
					tags: ['Food', 'Yummy', 'Delicious'],
					distance: 1.2,
					favorite: 0,
					image: 'https://i.pinimg.com/originals/9a/3d/35/9a3d355ecf245f984e6196695d55a7fe.png'
				},
				{	
					title: 'Title 2', 
					description: 'Something cool about this food truck that isn’t too long, gets the point across and helps explain what kind of food this truck is cookin up.',
					facebook:'facebook.com',
					twitter:'twitter.com',
					website:'google.com',
					phone:'555-555-5555',
					tags: ['Great', 'Ooo La La', 'Tasty'],
					distance: 1.2,
					favorite: 1,
					image: 'https://greendiningalliance.org/wp-content/uploads/2013/05/Food-Truck-Friday-Sauce-logo-300x300.jpg'
				},
				{	
					title: 'Really Long Title That I Want To Make Really Long Just To See How A Long Title Works', 
					description: 'Something cool about this food truck that isn’t too long, gets the point across and helps explain what kind of food this truck is cookin up.',
					facebook:'facebook.com',
					twitter:'twitter.com',
					website:'google.com',
					phone:'555-555-5555',
					tags: ['Food', 'Yummy', 'Delicious'],
					distance: 1.2,
					favorite: 0,
					image: 'https://i.pinimg.com/originals/9a/3d/35/9a3d355ecf245f984e6196695d55a7fe.png'
				},
				{	
					title: 'Title 4', 
					description: 'Something cool about this food truck that isn’t too long, gets the point across and helps explain what kind of food this truck is cookin up.',
					facebook:'facebook.com',
					twitter:'twitter.com',
					website:'google.com',
					phone:'555-555-5555',
					tags: ['Food', 'Yummy', 'Delicious'],
					distance: 1.2,
					favorite: 0,
					image: 'https://i.pinimg.com/originals/9a/3d/35/9a3d355ecf245f984e6196695d55a7fe.png'
				},
				{	
					title: 'Title 5', 
					description: 'Something cool about this food truck that isn’t too long, gets the point across and helps explain what kind of food this truck is cookin up.',
					facebook:'facebook.com',
					twitter:'twitter.com',
					website:'google.com',
					phone:'555-555-5555',
					tags: ['Chicken', 'Steak', 'Soup'],
					distance: 1.2,
					favorite: 1,
					image: 'https://greendiningalliance.org/wp-content/uploads/2013/05/Food-Truck-Friday-Sauce-logo-300x300.jpg'
				},
				{	
					title: 'John 6', 
					description: 'Something cool about this food truck that isn’t too long, gets the point across and helps explain what kind of food this truck is cookin up.',
					facebook:'facebook.com',
					twitter:'twitter.com',
					website:'google.com',
					phone:'555-555-5555',
					tags: ['Food', 'Yummy', 'Delicious'],
					distance: 1.2,
					favorite: 0,
					image: 'https://i.pinimg.com/originals/9a/3d/35/9a3d355ecf245f984e6196695d55a7fe.png'
				},
				{	
					title: 'Really Long Title That I Want To Make Really Long Just To See How A Long Title Works', 
					description: 'Something cool about this food truck that isn’t too long, gets the point across and helps explain what kind of food this truck is cookin up.',
					facebook:'facebook.com',
					twitter:'twitter.com',
					website:'google.com',
					phone:'555-555-5555',
					tags: ['Food', 'Yummy', 'Delicious'],
					distance: 1.2,
					favorite: 0,
					image: 'http://www.kindredpdx.com/wp-content/uploads/2013/08/CART-ROW-BW-LOGO.jpg'
				},
				{	
					title: 'Title 8', 
					description: 'Something cool about this food truck that isn’t too long, gets the point across and helps explain what kind of food this truck is cookin up.',
					facebook:'facebook.com',
					twitter:'twitter.com',
					website:'google.com',
					phone:'555-555-5555',
					tags: ['Food', 'Yummy', 'Delicious'],
					distance: 1.2,
					favorite: 0,
					image: 'https://i.pinimg.com/originals/9a/3d/35/9a3d355ecf245f984e6196695d55a7fe.png'
				},
				{	
					title: 'Title 9', 
					description: 'Something cool about this food truck that isn’t too long, gets the point across and helps explain what kind of food this truck is cookin up.',
					facebook:'facebook.com',
					twitter:'twitter.com',
					website:'google.com',
					phone:'555-555-5555',
					tags: ['Food', 'Yummy', 'Delicious'],
					distance: 1.2,
					favorite: 0,
					image: 'https://greendiningalliance.org/wp-content/uploads/2013/05/Food-Truck-Friday-Sauce-logo-300x300.jpg'
				},
				{	
					title: 'Title 10', 
					description: 'Something cool about this food truck that isn’t too long, gets the point across and helps explain what kind of food this truck is cookin up.',
					facebook:'facebook.com',
					twitter:'twitter.com',
					website:'google.com',
					phone:'555-555-5555',
					tags: ['Food', 'Yummy', 'Delicious'],
					distance: 1.2,
					favorite: 0,
					image: 'https://i.pinimg.com/originals/9a/3d/35/9a3d355ecf245f984e6196695d55a7fe.png'
				},
				{	
					title: 'Really Long Title That I Want To Make Really Long Just To See How A Long Title Works', 
					description: 'Something cool about this food truck that isn’t too long, gets the point across and helps explain what kind of food this truck is cookin up.',
					facebook:'facebook.com',
					twitter:'twitter.com',
					website:'google.com',
					phone:'555-555-5555',
					tags: ['Food', 'Yummy', 'Delicious'],
					distance: 1.2,
					favorite: 0,
					image: 'http://www.kindredpdx.com/wp-content/uploads/2013/08/CART-ROW-BW-LOGO.jpg'
				}
			)
			this.activeTrucks = this.trucks.length;
		},
		prevPage() {
			this.quickViewActive = null;
			this.loading = 1;
			if (this.activePage <= 1) {
				this.activePage = 1;
			} else {
				this.activePage = this.activePage - 1;
			}
			this.wp();
		},
		nextPage() {
			this.quickViewActive = null;
			this.loading = 1;
			if (this.activePage >= this.totalPages) {
				this.activePage = this.totalPages;
			} else {
				this.activePage = this.activePage + 1;
			}
			this.wp();
			
		},
		wp() {
			let url = 'https://ntknetwork.com/wp-json/wp/v2/pages?orderby=title&order=asc&page='+this.activePage+'&per_page='+this.perPage;
			axios
				.get(url)
				.then(response => {
					this.headers.push(response.headers)
					this.wordpress.push(response.data)
					this.loading = 0;
					this.activeTrucks = parseInt(this.headers[this.headers.length - 1]['x-wp-total']);
					this.totalPages = parseInt(this.headers[this.headers.length - 1]['x-wp-totalpages']);
					this.totalOnPage = this.wordpress[this.wordpress.length - 1].length;
				})
				.catch(error => {
					console.log(error)
				})
		}
	}, 
	created() {
		//this.updateList()
		this.wp()
	},
	components: {
		listViewItem,
		quickView
	}
}
</script>

<style scoped>
	.loading {margin-bottom:100%}
</style>