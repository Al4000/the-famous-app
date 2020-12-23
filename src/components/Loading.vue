<template>
	<div class="loading">
		<div class="loading__background"></div>
		<div class="loading__circles">
			<div class="loading__circle loading__circle--1"></div>
			<div class="loading__circle loading__circle--2"></div>
		</div>
	</div>
</template>

<script>
export default {
	name: "Loading"
}
</script>

<style lang="scss">
	$width: 64px;
	$height: 64px;

	.loading {
		position: fixed;
		top: 0;
		right: 0;
		left: 0;
		bottom: 0;
		&__background {
			width: 100%;
			height: 100%;
			background-color: rgba(#fff, 0.5);
		}
		&__circles {
			width: $width;
			height: $height;
			margin: auto;
			position: absolute;
			top: calc(50% - #{$width}/2);
			left: calc(50% - #{$height}/2);
		}
		&__circle {
			width: 100%;
			height: 100%;
			border-radius: 50%;
			background-color: #403432;
			opacity: 0.6;
			position: absolute;
			top: 0;
			left: 0;
			animation: loading-circles 2.0s infinite ease-in-out;
			&--2 {
				animation-delay: -1.0s;
			}
		}
	}

	@keyframes loading-circles {
		0%, 100% {
			transform: scale(0);
		}
		50% {
			transform: scale(1.0);
		}
	}
</style>
