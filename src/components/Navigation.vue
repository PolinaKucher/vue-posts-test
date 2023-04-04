<template>
	<div class="nav">
		<div class="btns">
			<my-button @click="$router.push('/')">Main</my-button>
			<my-button @click="$router.push('/posts')">Posts</my-button>
			<my-button @click="$router.push('/about')">About site</my-button>
			<my-button @click="$router.push('/store')">Store</my-button>
		</div>
	</div>
</template>

<script>
	export default {};
</script>

<style lang="scss" scoped>
	.nav {
		box-shadow: 2px 2px 4px grey;
		background-color: pink;
		height: 50px;
		display: flex;
		justify-content: space-between;
		align-items: center;
		gap: 10px;
	}

	.btns {
		margin-left: auto;
	}
</style>
