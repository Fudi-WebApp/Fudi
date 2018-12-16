<template>
	<div class="truck">
		<div class="logo">
			<a href="">
				<img :src="image" alt="">
			</a>
		</div>
		<div class="info">
			<h2><b v-html="title"></b><i @click="favoriteClick" v-if="star == 0" class="far fa-star"></i><i v-else-if="star == 1" @click="unfavoriteClick" class="fas fa-star"></i></h2>
			<p v-html="excerpt"></p>
			<div @click="showToggle" class="btn">{{showText}}</div>
			<br>
			<p v-if="show == 1" v-html="desc"></p>
			<span>
				<span class="tags" v-for="(tag, index) in tags">{{tag}}<span v-if="index != tags.length - 1">, </span></span>
				<span class="distance">{{distance}} miles away</span>
			</span>
		</div>
	</div>
</template>

<script>
export default {
  name: 'ListViewItem',
  props: ['title', 'desc', 'excerpt', 'tags', 'distance', 'favorite', 'image', 'slug'],
  data () {
    return {
      star: 0,
      show: 0,
      showText: 'Show More'
    }
  },
  methods: {
  	favoriteClick() {
  		if (this.star == 0) {
  			this.star = 1;
  		}
  	},
  	unfavoriteClick() {
  		if (this.star == 1) {
  			this.star = 0;
  		}
  	},
  	showToggle() {
  		if (this.show == 0) {
  			this.show = 1
  			this.showText = 'Show Less'
  		} else {
  			this.show = 0
  			this.showText = 'Show More'
  		}
  	}
  },
  created() {
  	this.star = this.favorite;
  }
}
</script>

<style scoped>
	.info h2 {display:flex; align-items:flex-start;}
	.info h2 b {margin-right:auto;}
	.info .far, .info .fal, .info .fas {margin-left:50px;}
	img {max-width:100%;}
</style>