<template>
	<div class="sc-message--text" :style="messageColors">
		<p v-html="messageText" class="sc-message--actual-message"></p>
		<p class='sc-message--meta' :style="{color: messageColors.color}">
			<span v-if="data.meta != null && data.meta.timestamp != null" class="timestamp-meta">
				{{data.meta.timestamp}}
			</span>
			<span v-else class="sc-message--pending"></span>
		</p>
	</div>
</template>

<script>
	import escapeGoat from 'escape-goat'
	import Autolinker from 'autolinker'
	const fmt = require('msgdown')

	export default {
		props: {
			data: {
				type: Object,
				required: true
			},
			messageColors: {
				type: Object,
				required: true
			},
			messageStyling: {
				type: Boolean,
				required: true
			}
		},
		methods: {
		},
		computed: {
			messageText() {
				const escaped = escapeGoat.escape(this.data.text)

				return Autolinker.link(this.messageStyling ? fmt(escaped) : escaped, {
					className: 'chatLink',
					truncate: {
						length: 50,
						location: 'smart'
					}
				})
			},
		}
	}
</script>

<style scoped>
	a.chatLink {
		color: inherit !important;
	}
	
</style>