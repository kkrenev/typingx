<template>
    <v-app id="app">
        <!-- <nav>
            <router-link to="/">Home</router-link> |
            <router-link to="/about">About</router-link>
        </nav> -->
        <v-container class="main">
            <router-view/>
        </v-container>
    </v-app>
</template>

<script>
    import '@/assets/main.scss';

    export default {};
</script>

<style lang="scss">
#app {
	font-family: Roboto, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	display: flex;
	justify-content: center;
	align-items: center;
	flex-direction: column;
	margin: 20px 0;

    .main {
        width: 800px;
    }
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
