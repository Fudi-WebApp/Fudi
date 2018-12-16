<template>
	<div class="quickViewContainer">
		<div class="logo">
			<a href=""><img :src="image" alt=""></a>
		</div>
		<div class="infoView">
			<div class="map">
				<img src="https://staticmapmaker.com/img/google@2x.png" alt="">
			</div>
			<div class="info">
				<h2 v-html="title"></h2>
				<p>{{phone}}
					<br><span v-for="(tag, index) in tags">{{tag}}<span v-if="index != tags.length - 1">, </span></span>
					<br><a href="">{{slug}}</a>
				</p>
				<p>
					<span class="socialContainer">
						<span class="social"><a href=""><i class="fab fa-facebook-f"></i></a></span>
						<span class="social"><a href=""><i class="fab fa-twitter"></i></a></span>
						<span class="social"><a href=""><i class="fab fa-instagram"></i></a></span>
					</span>
				</p>
				
				<div class="btn"><span>View More</span></div>
			</div>
		</div>
	</div>
</template>

<script>

export default {
  name: 'QuickView',
  props: ['title', 'facebook', 'twitter', 'website', 'phone', 'tags', 'image', 'slug'],
  data () {
    return {
      
    }
  }
}
</script>

<style scoped>
	img {max-width:100%;}
</style>