<template>
	<form @submit.prevent>
		<h4>Create post</h4>
		<my-input
			v-focus
			v-model="post.title"
			placeholder="Title" />
		<my-input
			v-model="post.body"
			placeholder="Description" />
		<my-button @click="createPost"> Add </my-button>
	</form>
</template>
<script>
	export default {
		data() {
			return {
				post: {
					title: "",
					body: "",
				},
			};
		},
		methods: {
			createPost() {
				this.post.id = Date.now();
				this.$emit("create", this.post);
				this.post = {
					title: "",
					body: "",
				};
			},
		},
		watch: {
			post: {
				handler(newValue) {
					console.log(newValue);
				},
				deep: true,
			},
		},
	};
</script>
<style scoped>
	form {
		margin-bottom: 40px;
		display: flex;
		flex-direction: column;
	}

	h4 {
		margin-bottom: 10px;
	}
</style>
