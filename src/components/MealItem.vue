<template>
  <div class="bg-white shadow rounded-xl">
				<router-link :to="{name: 'mealDetails', params: {id: meal.idMeal}}">
					<img :src="meal.strMealThumb" :alt="meal.strMeal" class="rounded-t-xl h-48 w-full object-cover">
				</router-link>
				<div class="p-3">
					<h3 class="font-semibold">{{ meal.strMeal }}</h3>
					<p class="mb-4">Lorem ipsum dolor sit amet consectetur adipisicing elit. Quidem cumque placeat illum alias blanditiis possimus.</p>
					<div class="flex justify-between items-center">
						<YouTubeButton :href="meal.strYoutube">Youtube</YouTubeButton>
					</div>
				</div>
			</div>
</template>

<script setup>
  import YouTubeButton from '../components/YouTubeButton.vue';
  const { meal } = defineProps({
    meal: Object
  })
</script>