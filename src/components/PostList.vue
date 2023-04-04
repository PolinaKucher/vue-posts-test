<template>
	<div v-show="posts.length > 0">
		<h3>User's list</h3>
		<transition-group name="post-list">
			<post-item
				v-for="post in posts"
				:post="post"
				:key="post.id"
				@remove="$emit('remove', post)" />
		</transition-group>
	</div>
	<h2 v-show="posts.length == 0">There is no posts</h2>
</template>
<script>
	import PostItem from "@/components/PostItem.vue";
	export default {
		components: { PostItem },
		props: {
			posts: {
				type: Array,
				required: true,
			},
		},
	};
</script>
<style scoped>
	h2 {
		color: rgb(178, 98, 114);
	}

	.post-list-item {
		display: inline-block;
		margin-right: 10px;
	}
	.post-list-enter-active,
	.post-list-leave-active {
		transition: all 0.5s ease-in-out;
	}
	.post-list-enter-from,
	.post-list-leave-to {
		opacity: 0;
		transform: translateX(30px);
	}

.post-list-move {
  transition: transform 0.8s ease;
}
</style>
