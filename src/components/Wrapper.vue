<template>
	<div class="main">
		<div class="inner">
			<h1 class="main__title">{{title}}</h1>
			<ul	class="main__cards" v-if="displayItems.length">
				<li
					class="main__card"
					v-for="(item, index) in displayItems"
					:key="index"
					:class="item.isSold ? 'sold' : ''"
				>
					<div class="main__card-img">
						<img :src="item.img" :alt="item.title">
					</div>
					<div class="main__card-info">
						<h2 class="main__card-title">
							{{item.title}}
						</h2>
						<div class="main__card-footer" v-if="!item.isSold">
							<div class="main__card-prices">
								<h6 v-if="item.old_price" class="main__card-price--old">{{item.old_price}}</h6>
								<h3 class="main__card-price">{{item.price}}</h3>
							</div>
							<div class="main__card-button">
								<button
									:class="item.inCart ? 'button--added' : ''"
									@click="handleClick(index, item.id)"
									:disabled="isLoading"
								>
									<span>{{item.inCart ? 'В корзине' : 'Купить'}}</span>
								</button>
							</div>
						</div>
						<div class="main__card-footer--sold" v-else>
							<h3>Продана на аукционе</h3>
						</div>
					</div>
				</li>
			</ul>
			<div class="main__empty" v-else>
				<h2>Картин по вашему запросу не найдено. Попробуйте изменить запрос</h2>
			</div>
		</div>
		<Loading v-if="isLoading" />
	</div>
</template>

<script>
import axios from 'axios'
import Loading from '@/components/Loading'

export default {
  name: 'Wrapper',
	components: {
		Loading
	},
	props: {
		searchQuery: String
	},
	created () {
		const inCartArray = JSON.parse(localStorage.getItem('Cart_items_ids')) || []
		if (inCartArray.length) {
			return this.cards.map(card => {
				if (inCartArray.indexOf(card.id) > -1) {
					return card.inCart = true
				}
			})
		}
	},
	data: () => ({
		isLoading: false,
		title: 'Картины эпохи Возрождения',
		cards: [
			{
				id: 1,
				img: require('@/assets/1.jpg'),
				title: '«Рождение Венеры» Сандро Боттичелли',
				price: '1 000 000 $',
				old_price: '2 000 000 $',
				inCart: false,
				isSold: false
			},
			{
				id: 2,
				img: require('@/assets/2.jpg'),
				title: '«Тайная вечеря»  Леонардо да Винчи',
				price: '3 000 000 $',
				old_price: false,
				inCart: false,
				isSold: false
			},
			{
				id: 3,
				img: require('@/assets/3.jpg'),
				title: '«Сотворение Адама» Микеланджело',
				price: '5 000 000 $',
				old_price: '6 000 000 $',
				inCart: false,
				isSold: false
			},
			{
				id: 4,
				img: require('@/assets/4.jpg'),
				title: '«Урок анатомии» Рембрандт',
				price: false,
				old_price: false,
				inCart: false,
				isSold: true
			}
		]
	}),
	methods: {
    handleClick (index, id) {
      this.isLoading = true
			const vm = this
			return new Promise((resolve, reject) => {
				axios
					.get('https://jsonplaceholder.typicode.com/posts/1')
					.then(function (response) {
						setTimeout(() => {
							vm.isLoading = false
							vm.cards[index].inCart = !vm.cards[index].inCart
							const inCartArray = JSON.parse(localStorage.getItem('Cart_items_ids')) || []
							const inCartIndex = inCartArray.indexOf(id)
							inCartArray.indexOf(id) > -1 ? inCartArray.splice(inCartIndex, 1) : inCartArray.push(id)
							localStorage.setItem('Cart_items_ids', JSON.stringify(inCartArray))
							resolve(response.data)
						}, 1000)
					})
					.catch((error) => {
						vm.isLoading = false
						reject(error)
					})
			})
    }
	},
	computed: {
		displayItems() {
			return this.cards.filter(item => item.title.toLowerCase().indexOf(this.searchQuery) !== -1)
		}
	}
}
</script>

<style scoped lang="scss">
	.main {
		min-height: calc(100vh - 193px);
		&__title {
			padding-top: 45px;
			margin-bottom: 39px;
		}
		&__empty {
			margin-top: 100px;
			text-align: center;
		}
		&__cards {
			display: flex;
		}
		&__card {
			border: 1px solid #E1E1E1;
			display: flex;
			flex-direction: column;
			margin-right: 32px;
			margin-bottom: 32px;
			width: 278px;
			&:nth-child(4n) {
				margin-right: 0;
			}
			&-title {
				margin-bottom: 22px;
				margin-top: 0;
			}
			&-info {
				padding: 20px 24px 24px;
				height: 100%;
			}
			&-price {
				white-space: nowrap;
				&--old {
					color: #A0A0A0;
					position: relative;
					display: inline-block;
					white-space: nowrap;
					&::before {
						content: '';
						position: absolute;
						left: 0;
						right: 0;
						top: 50%;
						height: 1px;
						background-color: #A0A0A0;
					}
				}
			}
			&-footer {
				display: flex;
				justify-content: space-between;
				align-items: center;
				&--sold {
					height: 48px;
					display: flex;
					align-items: center;
				}
			}
			&.sold {
				opacity: 0.5;
				cursor: not-allowed;
			}
		}
	}
</style>
