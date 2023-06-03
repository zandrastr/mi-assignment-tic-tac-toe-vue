<script setup lang="ts">
import { ref, Ref } from 'vue'; //imports ref function and Ref type from vue
import PlayerInput from './PlayerInput.vue';

let currentPlayer = ref(1);

let gameboardSquares= ref<string[]>( ['','','','','','','','','']);

console.log(gameboardSquares.value);

function placeSymbol(index: number){
    //add value of X or O to square
    //update current player

    console.log("placeSymbol", index);
    console.log(gameboardSquares.value[index]);
    console.log('currentPlayer --->', currentPlayer.value);

    if(currentPlayer.value === 1){
        gameboardSquares.value[index] = 'X';
        currentPlayer.value = 2;
    }
    else{
        gameboardSquares.value[index] = 'O';
        currentPlayer.value = 1;
    }
}
</script>

<!-- ********************************************************************************** -->

<template>
    <PlayerInput></PlayerInput>
    <div class="gameboardWrapper">
        <div class="gameboard">
            <div class="gameboardSquare" v-for="(square, index) in gameboardSquares" :key="index" @click.once="placeSymbol(index)"><p>{{ gameboardSquares[index] }}</p></div> <!-- List rendering, loops through the array, empty string  -->
        </div>
    </div>
</template>

<!-- ********************************************************************************** -->

<style scoped>
.gameboardWrapper {
    display: flex;
    justify-content: center;
}
.gameboard {
    width: 305px;
    height: 305px;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    position: relative;
}
.gameboardSquare {
    width: 100px;
    height: 100px;
    background: rgb(250, 250, 250);
    border: 1px solid black;
    margin: auto;
    display: flex;
    justify-content: center;
    align-items: center;
    font-weight: bold;
    font-size: 3rem;
}
</style>