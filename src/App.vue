<template>
	<navigation></navigation>
	<div class="app">
		<router-view></router-view>
	</div>
</template>

<script>
	import Navigation from "@/components/Navigation.vue";
	export default {
		components: {
			Navigation,
		},
	};
</script>

<style lang="scss">
	* {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	.app {
		padding: 20px;
	}
</style>
