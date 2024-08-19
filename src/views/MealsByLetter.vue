<template>
  <div class="p-8 pb-0">
    <h1 class="text-4xl font-bold text-green-600">Meals By Letter</h1>
    <div class="flex flex-wrap gap-2 mt-2 items-center justify-center">
      <router-link 
        :to="{ name: 'byLetter', params: { letter } }" 
        v-for="letter of letters" 
        :key="letter"
        class="hover:scale-110 hover:text-green-600 hover:font-bold px-1">
        {{ letter }}
      </router-link>
    </div>
    <Meals :meals="meals"/>
  </div>
</template>

<script setup>
import { computed, onMounted, watch } from 'vue';
import store from '../store';
import { useRoute } from 'vue-router';
import Meals from '../components/Meals.vue';

const route = useRoute();
const letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('')
const meals = computed(() => store.state.mealsByLetter)

watch(route, () => {
  store.dispatch('searchMealsByLetter', route.params.letter)
})

onMounted(() => {
  store.dispatch('searchMealsByLetter', route.params.letter)
})
</script>
