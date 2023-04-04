<template>
	<div class="post">
		<div>
			<div>{{ $store.state.likes }} likes</div>
			<div><strong>Title:</strong> {{ post.title }}</div>
			<div><strong>Description</strong> {{ post.body }}</div>
		</div>
		<div class="post__btns">
			<my-button @click="$router.push(`/posts/${post.id}`)">Open</my-button>
			<my-button @click="$emit('remove', post)">Delete</my-button>
		</div>
		<div class="post__id">{{ post.id }}</div>
	</div>
</template>
<script>
	export default {
		props: {
			post: {
				type: Object,
				required: true,
			},
		},
	};
</script>
<style lang="scss" scoped>
	.post {
		padding: 15px;
		border: 2px solid pink;
		margin-bottom: 15px;
		display: flex;
		align-items: center;
		justify-content: space-between;

		&__btns {
			display: flex;
			flex-direction: column;
			gap: 5px;
		}

		&__id {
			margin-left: 10px;
		}
	}
</style>
