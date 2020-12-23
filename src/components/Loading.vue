<template>
	<div class="loading">
		<div class="background"></div>
		<div class="sk-double-bounce">
			<div class="sk-child sk-double-bounce-1"></div>
			<div class="sk-child sk-double-bounce-2"></div>
		</div>
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
	}
	.background {
		width: 100%;
		height: 100%;
		background-color: rgba(#fff, 0.5);
	}
	.sk-double-bounce {
		width: 64px;
		height: 64px;
		margin: auto;
		position: absolute;
		top: calc(50% - 32px);
		left: calc(50% - 32px);
		.sk-child {
			width: 100%;
			height: 100%;
			border-radius: 50%;
			background-color: #403432;
			opacity: 0.6;
			position: absolute;
			top: 0;
			left: 0;
			animation: sk-double-bounce 2.0s infinite ease-in-out;
		}
		.sk-double-bounce-2 {
			animation-delay: -1.0s;
		}
	}

	@keyframes sk-double-bounce {
		0%, 100% {
			transform: scale(0);
		}
		50% {
			transform: scale(1.0);
		}
	}
</style>
