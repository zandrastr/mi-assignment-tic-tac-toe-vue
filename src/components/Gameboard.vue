<script setup lang="ts">
import { ref, Ref } from 'vue';
import PlayerInput from './PlayerInput.vue';

let userOneInput = ref('');
let userTwoInput = ref('');
let currentPlayer = ref(1);
let gameboardSquares= ref<string[]>( ['','','','','','','','','']);
let playerMessage = ref('');
let winnerMessage = ref('');
let isDraw: boolean = false;
let isGameOver: boolean = false;
let restartKey = ref(0);

function setPlayerNames(players: any) {
    userOneInput.value = players.userOne;
    userTwoInput.value = players.userTwo;
    addPlayerMessage();
}

function addPlayerMessage(){
    currentPlayer.value === 1 ? playerMessage.value = "It's your turn " + userOneInput.value + "!" : playerMessage.value = "It's your turn " + userTwoInput.value + "!";
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
    if(isGameOver === false) {
        if(gameboardSquares.value[0] !== '' && gameboardSquares.value[0] === gameboardSquares.value[1] && gameboardSquares.value[1] === gameboardSquares.value[2]){         
            winnerMessage.value = gameboardSquares.value[0] === 'X' ? userOneInput.value + " won!" : userTwoInput.value + " won!" ;
            isGameOver = true;
        }
        else if(gameboardSquares.value[3] !== '' && gameboardSquares.value[3] === gameboardSquares.value[4] && gameboardSquares.value[4] === gameboardSquares.value[5]){
            winnerMessage.value = gameboardSquares.value[3] === 'X' ? userOneInput.value + " won!" : userTwoInput.value + " won!" ;
            isGameOver = true;
        }
        else if(gameboardSquares.value[6] !== '' && gameboardSquares.value[6] === gameboardSquares.value[7] && gameboardSquares.value[7] === gameboardSquares.value[8]){
            winnerMessage.value = gameboardSquares.value[6] === 'X' ? userOneInput.value + " won!" : userTwoInput.value + " won!" ;
            isGameOver = true;
        }
        else if(gameboardSquares.value[0] !== '' && gameboardSquares.value[0] === gameboardSquares.value[3] && gameboardSquares.value[3] === gameboardSquares.value[6]){
            winnerMessage.value = gameboardSquares.value[0] === 'X' ? userOneInput.value + " won!" : userTwoInput.value + " won!" ;
            isGameOver = true;
        }
        else if(gameboardSquares.value[1] !== '' && gameboardSquares.value[1] === gameboardSquares.value[4] && gameboardSquares.value[4] === gameboardSquares.value[7]){
            winnerMessage.value = gameboardSquares.value[1] === 'X' ? userOneInput.value + " won!" : userTwoInput.value + " won!" ;
            isGameOver = true;
        }
        else if(gameboardSquares.value[2] !== '' && gameboardSquares.value[2] === gameboardSquares.value[5] && gameboardSquares.value[5] === gameboardSquares.value[8]){
            winnerMessage.value = gameboardSquares.value[2] === 'X' ? userOneInput.value + " won!" : userTwoInput.value + " won!" ;
            isGameOver = true;
        }
        else if(gameboardSquares.value[0] !== '' && gameboardSquares.value[0] === gameboardSquares.value[4] && gameboardSquares.value[4] === gameboardSquares.value[8]){
            winnerMessage.value = gameboardSquares.value[0] === 'X' ? userOneInput.value + " won!" : userTwoInput.value + " won!" ;
            isGameOver = true;
        }
        else if(gameboardSquares.value[2] !== '' && gameboardSquares.value[2] === gameboardSquares.value[4] && gameboardSquares.value[4] === gameboardSquares.value[6]){
            winnerMessage.value = gameboardSquares.value[2] === 'X' ? userOneInput.value + " won!" : userTwoInput.value + " won!" ;
            isGameOver = true;
        } 
        else if(gameboardSquares.value[0] !== '' 
        && gameboardSquares.value[1] !== '' 
        && gameboardSquares.value[2] !== '' 
        && gameboardSquares.value[3] !== '' 
        && gameboardSquares.value[4] !== '' 
        && gameboardSquares.value[5] !== '' 
        && gameboardSquares.value[6] !== '' 
        && gameboardSquares.value[7] !== '' 
        && gameboardSquares.value[8] !== ''){
            isGameOver = true;
            isDraw = true;
        }
    }
}

function playAgain(){
    restartKey.value += 1;
    userOneInput.value = '';
    userTwoInput.value = '';
    currentPlayer.value = 1;
    gameboardSquares.value = ['','','','','','','','',''];
    playerMessage.value = '';
    winnerMessage.value = '';
    isDraw = false;
    isGameOver = false;
}
</script>

<template>
    <PlayerInput :key="restartKey" @setPlayerNames="setPlayerNames"></PlayerInput>

    <div :key="restartKey" v-if="userOneInput !== '' && userOneInput !== '' " class="gameboardWrapper">
        <div class="gameboard" v-if="!isGameOver">
            <div class="gameboardSquare" v-if="!isGameOver" v-for="(square, index) in gameboardSquares" :key="index" @click.once="placeSymbol(index)"><p>{{ gameboardSquares[index] }}</p></div>
        </div>
        <p class="gameMsg" v-if="isGameOver && !isDraw" > {{ winnerMessage }} </p>
        <p class="gameMsg" v-if="isDraw === true"> It's a Tie! </p>
    </div>

    <p class="playerMsg" v-if="!isGameOver && !isDraw" > {{ playerMessage }} </p>
    <button class="gameOverBtn" v-if="isGameOver" @click="playAgain">Play again</button>    
</template>

<style scoped>
.gameboardWrapper {
    display: flex;
    flex-direction: column;
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
.playerMsg {
    font-size: 1.5rem;
    font-weight: bold;
    color: rgb(197, 21, 174);
}
.gameMsg {
    font-size: 3rem;
    font-weight: bold;
    color: rgb(197, 21, 174);
}
.gameOverBtn {
    padding: 7px;
    width: 40%;
    align-self: center;
    text-align: center;
    margin: 10px;
    background-color: rgb(26, 26, 102);
    color: aliceblue;
    border-radius: 5px;
    border: none;
}
.gameOverBtn:hover {
    background-color: rgb(197, 21, 174);
    color: aliceblue;
    border: none;
}
</style>