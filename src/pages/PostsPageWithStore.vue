<template>
	<div>
		<h1>{{ $store.state.post.limit }}</h1>
		<!-- <h1>Posts page</h1>
		<my-input
			v-focus
			v-model="searchQuery"
			placeholder="Searching..." />
		<div class="btns">
			<my-button @click="showDialog">Create post</my-button>
			<my-select
				v-model="selectedSort"
				:options="sortOptions" />
		</div>
		<my-dialog v-model:show="dialogVisible">
			<post-form @create="createPost" />
		</my-dialog>
		<post-list
			:posts="sortedAndSearchedPosts"
			@remove="removePost"
			v-if="!isPostsLoading" />
		<div v-else>Loading...</div>
		<div
			v-intersection="loadMorePosts"
			class="observer"></div> -->
	</div>
</template>

<script lang="js">
	import PostForm from "@/components/PostForm.vue";
	import PostList from "@/components/PostList.vue";
	import MyButton from "@/components/elements/MyButton.vue";
	import MySelect from "@/components/elements/MySelect.vue";
	import MyInput from "@/components/elements/MyInput.vue";

	export default {
		components: {
			PostForm,
			PostList,
			MyButton,
			MySelect,
			MyInput,
		},
		data() {
			return {
				posts: [],
				dialogVisible: false,
				isPostsLoading: false,
				selectedSort: "",
				searchQuery: "",
				page: 1,
				limit: 10,
				totalPages: 0,
				sortOptions: [
					{
						value: "title",
						name: "By title",
					},
					{
						value: "body",
						name: "By description",
					},
				],
			};
		},
		methods: {
			createPost(post) {
				this.posts.push(post);
				this.dialogVisible = false;
			},
			removePost(post) {
				this.posts = this.posts.filter((p) => p.id !== post.id);
			},
			showDialog() {
				this.dialogVisible = !this.dialogVisible;
			},

		},
	};
</script>

<style lang="scss">
	.btns {
		margin: 15px 0;
		display: flex;
		justify-content: space-between;
	}

	.page {
		border: 1px solid black;
		padding: 10px;
		margin-right: 10px;
		background-color: white;

		&:last-child {
			margin-right: 0;
		}

		&__wrapper {
			display: flex;
			margin-top: 15px;
		}

		&--current {
			border: 2px solid #509250;
		}
	}
</style>
