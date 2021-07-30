<template>
	<div class="app">
		<Header title="The Anime Quoter" />
		<Quote :quote="quote" />
		<div class="button-container">
			<button @click="fetchQuote">GET A NEW QUOTE</button>
		</div>
		<QuoteList :quotes="quotes" />
	</div>
</template>

<script>
import Header from './components/Header.vue';
import Quote from './components/Quote.vue';
import QuoteList from './components/QuoteList.vue';

export default {
	name: 'App',
	components: {
		Header,
		Quote,
		QuoteList
	},
	data() {
		return {
			quote: {
				content: '',
				character: '',
				anime: ''
			},
			quotes: []
		}
	},
	created () {
		this.fetchQuote();
	},
	methods: {
		async fetchQuote () {
			const data = await fetch('https://animechan.vercel.app/api/random').then(res => res.json());

			if (this.quote.content) {
				this.quotes = [...this.quotes, this.quote];
			}

			this.quote = {
				anime: data.anime,
				character: data.character,
				content: data.quote
			}
		}
	}
}
</script>

<style lang="scss">
:root {
	--primary: #4da844;
	--button: #468041;
	--secondary: #8164b9;
	--tertiary: #22a5d1;
	--dark: #e7e7e7;
	--verydark: rgb(182, 181, 181);
	--light: rgb(0, 0, 0);
	--grey: #929292;
}

* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
	font-family: 'Fira Sans', sans-serif;
}

.button-container {
	display: flex;
	justify-content: center;
	padding: 0px 32px;
	margin: 64px auto;

	button {
		border: none;
		outline: none;
		background-color: var(--primary);
		padding: 16px 32px;
		border-radius: 99px;

		color: var(--light);
		font-size: 1.5em;
		font-weight: 700;
		text-transform: uppercase;
		cursor: pointer;
		transition: 0.4s;

		&:hover {
			background-color: var(--button);
		}
	}
}
body {
  background-color: rgb(51, 51, 51);
}
</style>
