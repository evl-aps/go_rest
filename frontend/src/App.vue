<template>
<div>
	<h1>Tasks</h1>

	<div class="content">

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
}

body {
	background: rgb(180, 207, 241);
}

h1 {
	display: block;
	background: rgb(77, 120, 238);
	width: 95%;
	margin: 0 auto;
	text-align: center;
	color: #ffffff;
	border-radius: 5px;
	padding: 10px;
}

.content {
	display: flex;
	align-items: center;
	justify-content: space-between;
}
</style>
