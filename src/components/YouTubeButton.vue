<template>
  <a 
    :href="href" 
    target="_blank" 
    class="px-3 py-2 rounded border-2 text-white bg-green-500 border-green-500 hover:border-green-600 hover:bg-green-600 hover:cursor-pointer transition-colors"
  >
    <slot>Youtube</slot>
  </a>
</template>

<script setup>
const props = defineProps({
  href: String
})
</script>