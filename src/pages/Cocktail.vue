<script setup>
import axios from 'axios'
import { ref,computed } from 'vue'
import { useRoute } from 'vue-router'
import {COCKTAIL_BY_ID} from '../constants'
import AppLayout from '../components/AppLayout.vue'

const route = useRoute()

const cocktail = ref(null)
const cocktailId = computed(() => route.path.split("/").pop())

async function getCocktail(){
    const data = await axios.get(`${COCKTAIL_BY_ID}${cocktailId.value}`)
    cocktail.value = data?.data?.drinks[0]
    console.log(cocktail.value);
}

getCocktail()
</script>

<template>
    <div v-if="cocktail" class="wrap">
        <AppLayout :imgUrl="cocktail.strDrinkThumb">
            <div class="wrapper">
                <div class="info">
                    <div class="title">{{ cocktail.strDrink }}</div>
                    <div class="line"></div>
                </div>
            </div>
        </AppLayout>
    </div>
</template>

<style lang="sass" scoped>

@import '../assets/styles/main'


</style>