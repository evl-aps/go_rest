<template>
<div>
	<h1>Tasks</h1>

	<ul>
		<li v-for="task in tasks" :key="task.ID">
			{{task.Name}}
		</li>
	</ul>
	</div>
</template>

<script>
export default {
	name: 'App',

	data() {
		return {
			tasks: []
		}
	},

	mounted() {
		this.$http.get('http://localhost:8000/tasks')
		.then( response => {
			this.tasks = response.data.Tasks
		})
	}
}
</script>

<style>

</style>
