<script setup>
defineProps({
	keyName: String,
})
</script>

<template>
	<div>{{keyName}}</div>
</template>

<style scoped>
div {
	width: 70px;
	height: 70px;
	background-color: #333;
	border: 2px solid grey;
	border-radius: 10px;
	color: white;
	display: flex;
	align-items: center;
	justify-content: center;
	font-family: monospace;
}
</style>
