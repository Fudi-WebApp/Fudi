<template>
	<div class="truck">
		<div class="logo">
			<a href="">
				<img src="{{}}" alt="">
			</a>
		</div>
		<div class="info">
			<h2>{{title}}</h2>
			<p>{{desc}}</p>
			<span>
				<span class="tags">{{}}</span>
				<span class="distance">{{}}</span>
			</span>
		</div>
	</div>
</template>

<script>
export default {
  name: 'ListViewItem',
  props: ['title', 'desc'],
  data () {
    return {
      
    }
  }
}
</script>

<style scoped>

</style>