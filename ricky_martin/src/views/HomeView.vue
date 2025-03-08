<script setup lang="ts">
import { ref, onMounted, } from "vue";
import { useRouter } from "vue-router";
import type { Character } from "@/types/character";
    
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
    router.push(`/details/${character_id}`)
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
    <h1 class="text-3xl font-bold underline text-center mt-10">
        Ricky Martin Team!
    </h1>
    <div class="flex items-center space-x-4 justify-center text-center mt-10">
        <button @click="decrementePage" class="bg-blue-500 hover:bg-blue-600 text-white font-bold py-2 px-4 rounded-full shadow-lg transition duration-300 ease-in-out transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-opacity-50">-</button>
        {{ page }} 
        <button @click="incrementPage" class="bg-green-500 hover:bg-green-600 text-white font-bold py-2 px-4 rounded-full shadow-lg transition duration-300 ease-in-out transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-green-500 focus:ring-opacity-50">+</button>
    </div>

    <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 xl:grid-cols-6 gap-7 mt-24 mx-10">
        <div v-for="character in characters" :key="character.id">
            <div @click="seeCharacterDetails(character.id)">
                <img :src="character.image" alt="character.name"/>
                <h2>{{ character.name }}</h2>
            </div>
        </div>
    </div>


</template>

<style scoped>

</style>
