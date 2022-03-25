<script>
export default {
	// name: 'CustomButton',
	props: {
		text: {
			type: String,
			defualt: 'Add',
		},
		color: String,
	},
	methods: {
		// onClick() {
		// 	// console.log('clicked from the component')
		// },
	},
}
</script>

<template>
	<button
		:style="{ background: color }"
		class="btn"
		@click="$emit('btn-click')"
	>
		{{ text }}
	</button>
</template>
