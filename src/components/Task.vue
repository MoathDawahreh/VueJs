<script>
export default {
	name: 'User-Task',
	props: {
		task: Object,
	},
	methods: {
		// onDelete(id) {
		// 	this.$emit('delete-task', id)
		// 	// console.log('deletee', id)
		// },
	},
}
</script>

<template>
	<div
		:class="[task.reminder ? 'reminder' : '', 'task']"
		@dblclick="$emit('toggle-reminder')"
	>
		<h3>
			{{ task.text }}
			<i class="fas fa-times" @click="$emit('delete-task')"></i>
		</h3>
		<p>{{ task.day }}</p>
	</div>
</template>

<style scoped>
.fas {
	color: red;
}
.task {
	background: rgb(219, 203, 203);
	margin: 5px;
	padding: 10px 20px;
	cursor: pointer;
}
.task.reminder {
	border-left: 6px solid green;
}
.task h3 {
	display: flex;
	align-items: center;
	justify-content: space-between;
}
</style>
