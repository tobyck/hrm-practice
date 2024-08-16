<script setup>
import { ref, computed } from "vue"
import Key from "@/components/Key.vue"

const MODS = { Meta: .3, Control: .4, Alt: .3, Shift: .5, } 

// chords that can't be .preventDefault()'ed
const UNPREVENTABLE = [
	["Ctrl", "W"],
	["Ctrl", "N"],
	["Ctrl", "Shift", "P"],
	["Ctrl", "Shift", "W"]
]

const genChord = () => {
	const chord = Object.entries(MODS)
		.map(([mod, chance]) => Math.random() < chance ? mod : null)
		.filter(Boolean)
		.slice(0, 3) // 3 mods at most
		.concat("ABCDEFGHIJKLMNOPQRSTUVWXYZ"[~~(Math.random() * 26)])

	if (chord.length == 1) chord.unshift("Shift")

	if (UNPREVENTABLE.some(c => c.join() === chord.join())) return genChord()

	return chord;
}

const chord = ref(genChord())

// the `chord` ref has to have "Control" for .getModifierState to work
const displayedChord = computed(() => chord.value.map(key => key.replace("Control", "Ctrl")))

document.addEventListener("keydown", event => {
	event.preventDefault();

	if (
		(event.code === "Key" + chord.value.at(-1) &&
		Object.keys(MODS).every(mod => event.getModifierState(mod) || !chord.value.includes(mod))) ||
		event.code === "Enter"
	) chord.value = genChord()
})
</script>

<template>
	<div>
		<Key v-for="(key, index) in displayedChord" :key="index" :key-name="key" class="key"/>
	</div>
</template>

<style scoped>
div {
	display: flex;
	flex-flow: row;
	align-items: center;
	gap: 35px;
	position: relative;
}

.key:not(:last-child)::after {
	content: "+";
	color: lightgrey;
	position: absolute;
	display: block;
	left: 85px;
}
</style>
