<template>
  <div id="app">
		<Header />
		<Wrapper :searchQuery="searchQuery"/>
		<Footer />
  </div>
</template>

<script>
import Header from '@/components/Header'
import Wrapper from '@/components/Wrapper'
import Footer from '@/components/Footer'

export default {
  name: 'App',
  components: {
		Header, Wrapper, Footer
  },
	data: () => ({
		searchQuery: ''
	}),
	created () {
		this.$root.$on('search', this.searchHandle)
	},
	methods: {
		searchHandle (text) {
			this.searchQuery = text
		}
	}
}
</script>

<style>
#app {
  font-family: Merriweather, Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
	background: #F6F3F3;
	min-height: 100vh;
	color: #343030;
}
</style>
