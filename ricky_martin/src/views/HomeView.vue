<script setup lang="ts">
import { ref, onMounted, } from "vue";
import { useRouter } from "vue-router";
import { Character } from "../types/Character";
    
const router = useRouter();
const characters = ref<Character[]>([])
const page:any = ref<number>(1)


    const findCharacters = () => {
        loadCharacters()
    };

    const loadCharacters = async () => {
        const response = await fetch(`https://rickandmortyapi.com/api/character?page=${page.value}`)
        const data = await response.json()
        characters.value = data.results
        console.log();
    };

    const seeCharacterDetails =(character_id: number)=>{
        router.push(`details/${character_id}`)
    };
    
    const incrementPage = () => {
        if(page.value !== null){
            page.value++
            loadCharacters()
        }
    }

    const decrementePage = () => {
        if(page.value > 1){
        page.value--
        loadCharacters()
        }
    }

    onMounted(() => {
        loadCharacters()
    })
</script>

<template>

    <div>
        <button @click="incrementPage">+</button>
        {{ page }}
        <button @click="decrementePage">-</button>
    </div>

</template>

<style scoped>

</style>
