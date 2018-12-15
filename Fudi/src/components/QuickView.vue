<template>
	<div class="quickViewContainer">
		<div class="logo">
			<a href=""><img src="" alt=""></a>
		</div>
		<div class="infoView">
			<div class="map">
				<img src="https://staticmapmaker.com/img/google@2x.png" alt="">
			</div>
			<div class="info">
				<h2>{{}}</h2>
				<p>{{}}
					<br>{{}}
					<br><a href="">{{}}</a>
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
  
  data () {
    return {
      
    }
  }
}
</script>

<style scoped>

</style>