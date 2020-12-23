<template>
	<div class="footer">
		<div class="inner">
			<div class="footer__wrap">
				<Menu />
				<ul class="footer__info">
					<li class="footer__info-item">
						<img src="@/assets/phone.svg" alt="phone" class="footer__info-img">
						<a href="tel:+74955555555" class="footer__info-link">+7 (495) 555-55-55</a>
					</li>
					<li class="footer__info-item">
						<img src="@/assets/loc.svg" alt="pin" class="footer__info-img">
						<span>г. Москва, ул. Расплетина, 24</span>
					</li>
				</ul>
			</div>
		</div>
	</div>
</template>

<script>
import Menu from '@/components/Menu'

export default {
	name: "Footer",
	components: {
		Menu
	}
}
</script>

<style scoped lang="scss">
	.footer {
		background-color: #ECEAEA;
		height: 96px;
		display: flex;
		align-items: center;
		&__wrap {
			display: flex;
			align-items: center;
			justify-content: space-between;
		}
		&__info {
			display: flex;
			align-items: center;
			&-item {
				display: flex;
				align-items: center;
				color: #555;
				font-size: 14px;
				line-height: 21px;
				&:not(:first-child) {
					margin-left: 48px;
				}
			}
			&-link {
				transition: color 0.25s ease 0s;
				&:hover {
					color: lighten(#343030, 20%);
				}
			}
			&-img {
				margin-right: 11px;
				margin-top: 1px;
			}
		}
	}
</style>
