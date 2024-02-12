<template>
<div>
	<h1>Задачи</h1>

	<div class="content">
		<div class="content-item">
			<h2>Задачи</h2>

			<ul v-if="tasks.length">
				<li v-for="task in tasks" :key="task.ID">
					{{ task.Name }}
				</li>
			</ul>

			<button @click="getTasks">Обновить</button>
		</div>

		<div class="content-item">
			<h2>Добавить задачу</h2>

			<div class="form">
				<div>
					<label>Название</label>
					<input type="text">
				</div>

				<div>
					<label>Описание</label>
					<input type="text">
				</div>
			</div>

			<button>Добавить</button>
		</div>
	</div>

	<AppAlert v-for="(err, idx) in errors" type="error" :message="err" :key="idx" />
</div>
</template>

<script>
import AppAlert from './components/AppAlert.vue'

export default {
	name: 'App',

	components: { AppAlert },

	data() {
		return {
			tasks: [],
			errors: [],
		}
	},

	mounted() {
		this.getTasks()
	},

	methods: {
		async getTasks() {
			this.$http.get('http://localhost:8000/tasks')
			.then( response => {
				this.tasks = response.data.Tasks
			})
			.catch( err => this.errors = [...this.errors, err])
		}
	}
}
</script>

<style lang="scss">
* {
	font-family: Arial, Helvetica, sans-serif;
	margin: 0;
	padding: 0;
	color: #ffffff;
}

body {
	background: rgb(180, 207, 241);
}

h1 {
	display: block;
	background: rgb(77, 120, 238);
	width: 95%;
	margin: 20px auto 0 auto;
	text-align: center;
	color: #ffffff;
	border-radius: 5px;
	padding: 10px 0;
}

h2 {
	text-align: center;
}

button {
	border: none;
	outline: none;
	display: block;
	width: 50%;
	padding: 10px;
	font-size: 20px;
	border-radius: 5px;
	font-weight: 600;
	margin: 0 auto;
	background: #ffffff;
	color: rgb(77, 120, 238);
	cursor: pointer;
}

ul {
	list-style: none;
	text-align: center;
	font-weight: 600;
	padding: 20px 0;

	li {
		margin-bottom: 10px;
		cursor: pointer;
		border-radius: 5px;
		transition: all .35s ease;
		padding: 5px;

		&:hover {
			background: #ffffff;
			color: rgb(77, 120, 238);
		}

		&:last-child {
			margin-bottom: 0;
		}
	}
}

.content {
	width: 95%;
	margin: 0 auto;
	padding: 10px 0;
	display: flex;
	align-items: flex-start;
	justify-content: space-between;

	.content-item {
		width: 49%;
		padding: 10px;
		background: rgb(77, 120, 238);
		border-radius: 5px;
		box-sizing: border-box;
	}
}

.form {
	padding: 20px 0;

	div {
		margin-bottom: 10px;

		&:last-child {
			margin-bottom: 0;
		}

		label {
			font-weight: 600;
			margin-bottom: 3px;
		}

		input {
			display: block;
			width: 100%;
			padding: 10px;
			box-sizing: border-box;
			border-radius: 5px;
			border: none;
			outline: none;
			color: rgb(77, 120, 238);
			font-size: 16px;
			font-weight: 600;
		}
	}
}
</style>
