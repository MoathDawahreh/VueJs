<script>
import CustomButton from './CustomButton.vue'
export default {
	name: 'TrackerHeader',
	props: {
		title: {
			type: String,
			default: 'Moath Task tracker',
		},
		showAddTask: {
			type: Boolean,
		},
	},
	components: {
		CustomButton,
	},
	methods: {
		// logOut() {
		// 	console.log('log out clicked!')
		// },
		addTask() {
			console.log('addtask clicked!')
		},
	},
}
</script>
<template>
	<header>
		<h1>{{ title }}</h1>
		<CustomButton
			:text="showAddTask ? 'Close' : 'Add Task'"
			:color="showAddTask ? 'red' : 'green'"
			@btn-click="$emit('Add-task')"
		/>
		<CustomButton text="Log out" color="gray" @btn-click="$emit('log-out')" />
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
