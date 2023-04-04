<template>
	<button>
		<slot></slot>
	</button>
</template>

<script>
	export default {
		name: 'my-button'
	};
</script>

<style lang="scss" scoped>
	button {
		width: 80px;
		height: 40px;
		border: none;
		color: white;
		border-radius: 4px;
		align-self: flex-end;
		background-color: pink;
	}
</style>
