<template>
  <h1 class="p-8 text-4xl font-bold text-green-600">Meals for {{ ingredient.strIngredient }}</h1>
  <Meals :meals="meals"/>
</template>

<script setup>
import { computed, onMounted, ref } from 'vue';
import axiosClient from '../axiosClient';
import store from '../store';
import { useRoute } from 'vue-router';
import Meals from "../components/Meals.vue";

const route = useRoute();
onMounted(() => {
  store.dispatch('searchMealsByIngredients', route.params.ingredients)
})
const meals = computed(() => store.state.mealsByIngredients)
const ingredient = computed(() => store.state.ingredient)
</script>
