<template>
	<div class="header">
		<div class="inner">
			<div class="header__wrap">
				<Menu />
				<div class="header__search">
					<input
						type="text"
						class="header__search-input"
						placeholder="Поиск по названию картины"
						v-model="search"
						@keyup.enter="handleSearch"
					>
					<button
						class="header__search-button"
						@click="handleSearch"
					>
						<span>Найти</span>
					</button>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import Menu from '@/components/Menu'

export default {
	name: "Header",
	components: {
		Menu
	},
	data: () => ({
		search: ''
	}),
	methods: {
		handleSearch () {
			this.$root.$emit('search', this.search.toLowerCase())
		}
	}
}
</script>

<style scoped lang="scss">
	.header {
		height: 96px;
		border-bottom: 1px solid #e1e1e1;
		display: flex;
		align-items: center;
		&__wrap {
			display: flex;
			align-items: center;
			justify-content: space-between;
		}
		&__search {
			margin-left: auto;
			&-button {
				width: 122px;
			}
		}
	}
</style>