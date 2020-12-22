<template>
	<div class="menu__wrap">
		<div class="menu__logo">
			<img src="@/assets/logo.svg" alt="logo">
		</div>
		<ul class="menu__list">
			<li
				v-for="(item, index) in menu"
				:key="index"
				class="menu__list-item"
			>{{item}}</li>
		</ul>
	</div>
</template>

<script>
export default {
	name: "Menu",
	data: () => ({
		menu: [
			'Каталог',
			'Доставка',
			'Оплата',
			'Контакты',
			'О галерее'
		]
	})
}
</script>

<style lang="scss">
	.menu {
		&__wrap {
			display: flex;
			align-items: center;
		}
		&__list {
			display: flex;
			align-items: center;
			&-item {
				font-size: 14px;
				line-height: 21px;
				margin-left: 48px;
				cursor: pointer;
				transition: color 0.3s ease 0s;
				&:hover {
					color: lighten(#343030, 20%);
				}
			}
		}
	}
</style>