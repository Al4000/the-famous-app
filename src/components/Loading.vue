<template>
	<div class="loading">
		<div class="background"></div>
		<img src="@/assets/loading.gif" alt="" class="loading__img">
	</div>
</template>

<script>
export default {
	name: "Loading"
}
</script>

<style lang="scss">
	.loading {
		position: fixed;
		top: 0;
		right: 0;
		left: 0;
		bottom: 0;
		&__img {
			position: absolute;
			top: calc(50% - 32px);
			left: calc(50% - 32px);
		}
	}
	.background {
		width: 100%;
		height: 100%;
		background-color: rgba(#fff, 0.5);
	}
</style>