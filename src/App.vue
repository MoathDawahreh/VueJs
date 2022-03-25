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
		deleteTask(id) {
			// console.log('task', id)
			if (confirm('Delete the Task?')) {
				this.tasks = this.tasks.filter((task) => task.id !== id)
			}
		},
		toggleReminder(id) {
			this.tasks = this.tasks.map((task) =>
				task.id == id ? { ...task, reminder: !task.reminder } : task
			)
			console.log('reminder', id)
		},
		newTask(newTask) {
			this.tasks = [...this.tasks, newTask]
		},
		addToggle() {
			this.showAddTask = !this.showAddTask
		},
	},
	created() {
		this.tasks = [
			{
				id: '1',
				text: 'Doctors Appointment',
				day: 'March 5th at 2:30pm',
				reminder: true,
			},
			{
				id: '2',
				text: 'Meeting with boss',
				day: 'March 6th at 1:30pm',
				reminder: true,
			},
			{
				id: '3',
				text: 'Food shopping',
				day: 'March 7th at 2:00pm',
				reminder: false,
			},
		]
	},
	emits: ['add-task', 'on-click'],
}
</script>

<template>
	<div class="container">
		<TrackerHeader title="Task Tracker" @on-click="addToggle" />
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
	padding: 10px 20px;
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
