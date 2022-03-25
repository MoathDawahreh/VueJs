<script>
import TrackerHeader from './components/TrackerHeader.vue'
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'
export default {
	// name: 'App',
	components: {
		TrackerHeader,
		Tasks,
		AddTask,
	},
	data() {
		return {
			tasks: [],
			showAddTask: false,
		}
	},
	methods: {
		async deleteTask(id) {
			if (confirm('Delete the Task?')) {
				const res = await fetch(`api/tasks/${id}`, {
					method: 'DELETE',
				})

				res.status == 200
					? (this.tasks = this.tasks.filter((task) => task.id !== id))
					: alert('errorr')
				return res
			}
		},
		async toggleReminder(id) {
			const taskToToggle = await this.fetchTask(id)
			const updatedTask = { ...taskToToggle, reminder: !taskToToggle.reminder }

			const res = await fetch(`api/tasks/${id}`, {
				method: 'PUT',
				headers: {
					'Content-type': 'application/json',
				},
				body: JSON.stringify(updatedTask),
			})

			const data = await res.json()

			this.tasks = this.tasks.map((task) =>
				task.id == id ? { ...task, reminder: data.reminder } : task
			)
		},
		async fetchTasks() {
			const res = await fetch('api/tasks')
			const data = await res.json()

			return data
		},
		async fetchTask(id) {
			const res = await fetch(`api/tasks/${id}`)
			const data = await res.json()

			return data
		},
		async newTask(newTask) {
			const res = await fetch('api/tasks', {
				method: 'POST',
				headers: {
					'Content-type': 'application/json',
				},
				body: JSON.stringify(newTask),
			})
			const data = await res.json()
			this.tasks = [...this.tasks, data]
		},
		addToggle() {
			this.showAddTask = !this.showAddTask
		},
		logOut() {
			console.log('log out clicked!')
		},
	},
	async created() {
		this.tasks = await this.fetchTasks()
	},
	// emits: ['add-task'],
}
</script>

<template>
	<div class="container">
		<TrackerHeader
			title="Task Tracker"
			@Add-task="addToggle"
			@log-out="logOut"
			:showAddTask="showAddTask"
		/>
		<div v-show="showAddTask">
			<AddTask @add-task="newTask" />
		</div>
		<Tasks
			:tasks="tasks"
			@delete-task="deleteTask"
			@toggle-reminder="toggleReminder"
		/>
	</div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

/* #app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
} */

* {
	box-sizing: border-box;
	margin: 0;
	padding: 0;
}
body {
	/* font-family: 'Poppins', sans-serif; */
	font-family: Avenir, Helvetica, Arial, sans-serif;
}
.container {
	max-width: 500px;
	min-width: 300px;
	margin: 30px auto;
	overflow: auto;
	min-height: 300px;
	border: 1px solid steelblue;
	padding: 30px;
	border-radius: 5px;
}
.btn {
	display: inline-block;
	background: #000;
	color: #fff;
	border: none;
	padding: 10px 10px;
	margin: 5px;
	border-radius: 5px;
	cursor: pointer;
	text-decoration: none;
	font-size: 15px;
	font-family: inherit;
}
.btn:focus {
	outline: none;
}
.btn:active {
	transform: scale(0.98);
}
.btn-block {
	display: block;
	width: 100%;
}
</style>
