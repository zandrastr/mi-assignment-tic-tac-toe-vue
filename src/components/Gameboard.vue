<script setup lang="ts">
import { ref, Ref } from 'vue'; //imports ref function and Ref type from vue
import PlayerInput from './PlayerInput.vue';

let userOneInput = ref('');
let userTwoInput = ref('');
let currentPlayer = ref(1);
let gameboardSquares= ref<string[]>( ['','','','','','','','','']);
let playerMessage = ref('');
let winnerMessage = ref('');
let isDraw: boolean = false;
let isGameOver: boolean = false;

function setPlayerNames(players: any) {
    userOneInput.value = players.userOne;
    userTwoInput.value = players.userTwo;
    console.log('User One Input:', userOneInput.value);
    console.log('User Two Input:', userTwoInput.value);
    addPlayerMessage();
}

function addPlayerMessage(){
    currentPlayer.value === 1 ? playerMessage.value = "Its your turn " + userOneInput.value + "!" : playerMessage.value = "Its your turn " + userTwoInput.value + "!";
}

function placeSymbol(index: number){
    if(currentPlayer.value === 1){
        gameboardSquares.value[index] = 'X';
        currentPlayer.value = 2;
        addPlayerMessage();
        winnerCalculator();
    }
    else{
        gameboardSquares.value[index] = 'O';
        currentPlayer.value = 1;
        addPlayerMessage();
        winnerCalculator();
    }
}

function winnerCalculator(){
    console.log("Winner calculator");
}
</script>

<!-- ********************************************************************************** -->

<template>
    <PlayerInput @setPlayerNames="setPlayerNames"></PlayerInput>
    <div class="gameboardWrapper">
        <div class="gameboard">
            <div class="gameboardSquare" v-if="!isGameOver" v-for="(square, index) in gameboardSquares" :key="index" @click.once="placeSymbol(index)"><p>{{ gameboardSquares[index] }}</p></div> <!-- List rendering, loops through the array, empty string  -->
            <p v-if="isGameOver">Play again</p>
        </div>
    </div>
    <p v-if="!isGameOver && !isDraw" > {{ playerMessage }} </p>
    <p v-if="isGameOver && !isDraw" > {{ winnerMessage }} </p>
    <p v-if="isDraw === true"> It's a Tie! </p>

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