<script setup>
import AppLayout from '../components/AppLayout.vue'
import CocktailThumb from '../components/CocktailThumb.vue'
import { useRootStore } from '@/stores/root'
import { storeToRefs } from 'pinia';

const rootStore = useRootStore()
rootStore.getIngredients()

const { ingredients, ingredient, cocktails } = storeToRefs(rootStore)
 
function getCocktails() {
    rootStore.getCocktails(rootStore.ingredient)
}
</script>

<template>
    <AppLayout imgUrl="/src/assets/img/dawa-cocktail.jpg">
        <div class="wrapper">
            <div v-if="!ingredient || !cocktails" class="info">
                <div class="title">Выбери свой напиток &#128521;</div>
                <div class="line"></div>

                <div class="select-wrapper">
                    <el-select 
                        v-model="rootStore.ingredient" 
                        placeholder="Выбери основной ингредиент" 
                        size="large"
                        filterable 
                        allow-create
                        class="select"
                        @change="getCocktails"
                        >

                        <el-option
                        v-for="item in ingredients"
                        :key="item.strIngredient1"
                        :label="item.strIngredient1"
                        :value="item.strIngredient1"
                        />
                    </el-select>
                </div>
                 <div class="text">
                    Попробуйте наши вкусные рецепты коктейлей на любой случай. Найдите рецепты вкусных коктейлей по ингредиентам с помощью нашего генератора коктейлей.
                 </div>
                 <img src="/src/assets/img/shot-kokteil.png" alt="cocktails" class="img">
            </div>
            <div v-else class="info">
                <div class="title">COCKTAILS {{ ingredient }} &#128521;</div>
                <div class="line"></div>
                <div class="cocktails">
                    <CocktailThumb v-for="cocktail in cocktails"
                    :key="cocktail.idDrink"
                    :cocktail="cocktail"
                    />
                </div>
            </div>
        </div>
    </AppLayout>
</template>

<style lang="sass" scoped>

@import '../assets/styles/main'



.select-wrapper
    padding-top: 50px
    
.select
    width: 220px
.text
    max-width: 516px
    margin: 0 auto
    padding-top: 50px
    line-height: 36px
    letter-spacing: 0.1em
    color: $textMuted

.img
    margin-top: 60px

.cocktails
    display: flex
    align-items: center
    flex-wrap: wrap
    max-height: 400px
    overflow-y: auto
    margin-top: 60px
</style>