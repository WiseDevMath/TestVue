<script setup>
const props = defineProps({
  livre: Object
})
</script>

<template>
    <li>{{ livre.titre }} - {{ livre.auteur }} </li>
</template>