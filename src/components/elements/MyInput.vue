<template>
	<input
		:value="modelValue"
		@input="updateInput"
		class="input"
		type="text" />
</template>

<script>
	export default {
		name: "my-input",
		props: {
			modelValue: [String, Number],
		},
    methods: {
      updateInput(event) {
        this.$emit('update:modelValue', event.target.value)
      }
    }
	};
</script>

<style lang="scss" scoped>
	.input {
		margin-top: 10px;
		margin-bottom: 10px;
		width: 100%;
		padding: 12px 5px;
		margin-right: 10px;
		border-radius: 4px;
		border: 1px solid pink;
	}
</style>
