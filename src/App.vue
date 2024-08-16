<script setup>
import Game from "@/components/Game.vue"
</script>

<template>
	<main>
		<Game/>
		<p>Press enter to skip</p>
	</main>
</template>

<style>
body {
	margin: 0;
	background-color: #191919;
}

main {
	display: flex;
	align-items: center;
	justify-content: center;
	height: 100vh;
}

p {
	position: absolute;
	bottom: 50px;
	color: lightgrey;
	font-family: monospace;
}
</style>
