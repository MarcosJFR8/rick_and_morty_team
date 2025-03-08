<script setup lang="ts">
import { ref } from 'vue'


const characters = ref(['Rick', 'Morty', 'Summer', 'Beth', 'Jerry'])





</script>

<template>
    <div v-for="character in characters" :key="character.id">
        <h2>{{ character }}</h2>



    </div>

</template>

<style scoped>

</style>
