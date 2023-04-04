<template>
	<div
		class="dialog"
		v-if="show"
		@click="hideDialog">
		<div
			@click.stop
			class="content">
			<slot></slot>
		</div>
	</div>
</template>

<script>
	import toggleMixin from "@/mixins/toggleMixin";

	export default {
		name: "my-dialog",
		mixins: [toggleMixin],
    mounted() {
      console.log('dialog mounted!')
    }
	};
</script>

<style lang="scss" scoped>
	.dialog {
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		display: flex;
		position: fixed;
		background-color: rgba($color: #000000, $alpha: 0.5);
	}

	.content {
		margin: auto;
		background-color: rgb(254, 232, 235);
		padding: 20px;
		border-radius: 12px;
		min-height: 50px;
		min-width: 300px;
	}
</style>
