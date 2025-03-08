<script setup lang="ts">
import { ref, onMounted, } from "vue";
import { useRouter } from "vue-router";
    
const router = useRouter();
const characters = ref<Character[]>([])


    const findCharacters = () => {
        loadCharacters()
    };

    const loadCharacters = async () => {
        const response = await fetch(`https://rickandmortyapi.com/api/character/`)
        const data = await response.json()
        characters.value = data.results
        console.log();
    };

    const seeCharacterDetails =(character_id: number)=>{
        router.push(`details/${character_id}`)
    };   

    onMounted(() => {
        loadCharacters()
    })
</script>

<template>

</template>
