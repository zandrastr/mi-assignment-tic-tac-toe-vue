<script setup lang="ts">
import { ref, Ref } from 'vue'; //imports ref function and Ref type from vue

// The numbers in gameboardSquares array:
// 0 = square has not been clicked on yet
// When a player clicks a square, value gets updated to:
// 1 = if player 1 clicked
// 2  = if player 2 clicked
let gameboardSquares: Ref<number[]> = ref([0,0,0,0,0,0,0,0,0]);
console.log(gameboardSquares.value);

</script>

<!-- ********************************************************************************** -->

<template>
    <div class="gameboardWrapper">
        <div class="gameboard">
            <div class="gameboardSquare" v-for="(square, index) in gameboardSquares" :key="index">{{ '' }}</div> <!-- List rendering, loops through the array, empty string  -->
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
}
</style>