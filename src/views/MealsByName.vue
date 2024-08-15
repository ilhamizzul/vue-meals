<template>
		<div class="p-8 pb-0">
				<input
						type="text"
						v-model="keyword"
						class="rounded border-2 border-gray-200 w-full"
						placeholder="Search for Meals"
						@change="searchMeals"
				/>
		</div>
		<div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-8">
			<div v-for="meal of meals" :key="meal.idMeal" class="bg-white shadow rounded-xl">
				<router-link to="/">
					<img :src="meal.strMealThumb" :alt="strMeal" class="rounded-t-xl h-48 w-full object-cover">
				</router-link>
				<div class="p-3">
					<h3 class="font-semibold">{{ meal.strMeal }}</h3>
					<p class="mb-4">Lorem ipsum dolor sit amet consectetur adipisicing elit. Quidem cumque placeat illum alias blanditiis possimus.</p>
					<div class="flex justify-between items-center">
						<a 
							:href="meal.strYoutube" 
							target="_blank" 
							class="px-3 py-2 rounded border border-2 text-white bg-red-500 border-red-600 hover:bg-red-600 hover:cursor-pointer transition-colors"
						>
							YouTube
						</a>
					</div>
				</div>
			</div>
		</div>
</template>

<script setup>
	import { computed, onMounted, ref } from 'vue';
	import axiosClient from '../axiosClient';
	import store from '../store';
import { useRoute } from 'vue-router';

	const route = useRoute();
	const keyword = ref('');
	const meals = computed(() => store.state.searchedMeals)

	function searchMeals() {
		store.dispatch('searchMeals', keyword.value)
	}

	onMounted(() => {
		keyword.value = route.params.name
		if (keyword.value) {
			searchMeals()
		}
	})
</script>
