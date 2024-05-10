<template>
<div id="app">
	<nav>
		<router-link to="/">Home</router-link> |
		<router-link to="/about">About</router-link>
	</nav>
	<router-view/>
</div>
</template>

<script>
import Vue from 'vue';

export default {
	beforeCreate() {
		Vue.prototype.$app = this;
	},
	methods: {
		async openUrlAtAnotherDisplay(url) {
			const screenDetails = await window.getScreenDetails();
			const { currentScreen, screens } = screenDetails;
			if (screens.length === 1) return;
			const anotherScreen = screens.filter((screen) => screen !== currentScreen)[0];
			const { width, height, left, top } = anotherScreen;
			window.newWindow = window.open(url, 'about', `width=${width},height=${height},left=${left},top=${top},fullscreen=yes`);
		}
	},
}
</script>

<style lang="scss">
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
}

nav {
	padding: 30px;

	a {
		font-weight: bold;
		color: #2c3e50;

		&.router-link-exact-active {
			color: #42b983;
		}
	}
}
</style>
