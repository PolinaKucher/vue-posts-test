<template>
	<div>
		<h1>Posts page</h1>
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
			class="observer"></div>
	</div>
</template>

<script>
	import PostForm from "@/components/PostForm.vue";
	import PostList from "@/components/PostList.vue";
	import MyButton from "@/components/elements/MyButton.vue";
	import axios from "axios";
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
			async fetchPosts() {
				try {
					this.isPostsLoading = true;
					const response = await axios.get(
						"https://jsonplaceholder.typicode.com/posts",
						{
							params: {
								_page: this.page,
								_limit: this.limit,
							},
						}
					);
					this.totalPages = Math.ceil(
						response.headers["x-total-count"] / this.limit
					);
					this.posts = response.data;
				} catch (e) {
					alert("Error!");
				} finally {
					this.isPostsLoading = false;
				}
			},
			async loadMorePosts() {
				try {
					this.page += 1;
					const response = await axios.get(
						"https://jsonplaceholder.typicode.com/posts",
						{
							params: {
								_page: this.page,
								_limit: this.limit,
							},
						}
					);
					this.totalPages = Math.ceil(
						response.headers["x-total-count"] / this.limit
					);
					this.posts = [...this.posts, ...response.data];
				} catch (e) {
					alert("Error!");
				}
			},
		},
		mounted() {
			this.fetchPosts();
		},
		computed: {
			sortedPosts() {
				return [...this.posts].sort((post1, post2) =>
					post1[this.selectedSort]?.localeCompare(post2[this.selectedSort])
				);
			},
			sortedAndSearchedPosts() {
				return this.sortedPosts.filter((post) =>
					post.title.toLowerCase().includes(this.searchQuery.toLowerCase())
				);
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
