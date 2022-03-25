<script>
import CustomButton from './CustomButton.vue'
export default {
	name: 'TrackerHeader',
	props: {
		title: {
			type: String,
			default: 'Moath Task tracker',
		},
	},
	components: {
		CustomButton,
	},
	methods: {
		logOut() {
			console.log('log out clicked!')
		},
		addTask() {
			console.log('addtask clicked!')
		},
	},
}
</script>
<template>
	<header>
		<h1>{{ title }}</h1>
		<CustomButton text="Add Task" color="green" @on-click="$emit('onClick')" />
		<CustomButton text="Log out" color="gray" @on-click="logOut" />
	</header>
</template>

<style scoped>
header {
	display: flex;
	justify-content: space-between;
	align-items: center;
	margin: 10 20px;
}
</style>
