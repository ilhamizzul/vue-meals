<template>
	<div class="p-8 pb-0 text-green-600">
		<h1 class="text-4xl font-bold mb-4">Random Meals</h1>
	</div>
	<Meals :meals="meals"/>
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import store from '../store'
import axiosClient from "../axiosClient";
import Meals from "../components/Meals.vue";

const meals = ref([])

onMounted(async () => {
	for (let i = 0; i < 10; i++) {
		await axiosClient.get(`random.php`)
			.then(({ data }) => meals.value.push(data.meals[0]));
	}
})
</script>
