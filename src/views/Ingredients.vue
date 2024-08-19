<template>
  <div class="p-8">
    <h1 class="text-4xl font-bold mb-4 text-green-600">Ingredients</h1>
    <input
        type="text"
        v-model="keyword"
        class="rounded border-2 border-gray-200 w-full mb-3 focus:ring-green-600 focus:border-green-600"
        placeholder="Search for Ingredients"
    />
    <div class="grid grid-cols-1 md:grid-cols-2 gap-x-2">
      <a href="#"
        v-for="ingredient of computedIngredients" 
        @click.prevent="openIngredient(ingredient)"
        :to="{name: 'byIngredient', params: {ingredients: ingredient.strIngredient}}"
        :key="ingredient.idIngredient" 
        class="block bg-white rounded p-3 mb-3 shadow hover:cursor-pointer transition-all hover:bg-green-600 hover:text-white">
        <h3 class="text-2xl font-bold mb-2">{{ ingredient.strIngredient }}</h3>
      </a>
    </div>
  </div>
</template>

<script setup>
import { computed, onMounted, ref } from 'vue';
import axiosClient from '../axiosClient';
import { useRoute, useRouter } from 'vue-router';
import store from '../store';

const router = useRouter()
const ingredients = ref([])
const keyword = ref('')

const computedIngredients = computed(() => {
  if (!computedIngredients) return ingredients
  return ingredients.value.filter(
    i => i.strIngredient.toLowerCase().includes(keyword.value.toLowerCase())
  )
})

function openIngredient(ingredient) {
  store.commit('setIngredient', ingredient)
  router.push({
    name: 'byIngredient',
    params: {
      ingredients: ingredient.strIngredient
    }
  })
}

onMounted(() => {
  axiosClient.get('list.php?i=list')
  .then(({data}) => ingredients.value = data.meals)
})
</script>
