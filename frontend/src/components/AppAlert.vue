<template>
	<div
		class="alert"
		:class="{ 'error': type == 'error', 'warning': type == 'warning', 'success': type == 'success' }"
	>
		{{ message }}
	</div>
</template>

<script>
export default {
	name: 'AppAlert',

	props: {
		type: String,
		message: String,
	},
}
</script>

<style lang="scss" scoped>
.alert {
	width: 40%;
	padding: 10px;
	position: fixed;
	top: 10px;
	left: 50%;
	transform: translateX(-50%);
	border-radius: 5px;
	z-index: 100;
	color: #ffffff;
	font-size: 18px;
	font-weight: 600;
	text-align: center;

	&.error {
		background: rgb(226, 52, 52);
		border-top: 10px solid rgb(185, 63, 63);
	}
}
</style>