<script setup lang="ts">
import { ref } from 'vue'; //imports ref function from vue

const userOneInput = ref("");  
const userTwoInput = ref(""); 
const isSubmitted = ref(false); //to keep track if inputs are submitted or not

const emits = defineEmits(['setPlayerNames']);

//if inputs are not empty, set isSubmitted value to true
function handleSubmit() {
    if(userOneInput.value !== '' && userTwoInput.value !== ''){
        isSubmitted.value = true;
        emits('setPlayerNames', {
            userOne: userOneInput.value,
            userTwo: userTwoInput.value
        });
    }
};

</script>

<!-- ********************************************************************************** -->

<template>

    <div class="playerInput" v-if="!isSubmitted"> <!-- if inputs are not submitted yet, show input fields-->
        <p>ADD PLAYER NAMES</p>
        <input type="text" placeholder="Player 1" v-model="userOneInput"/>
        <input type="text" placeholder="Player 2" v-model="userTwoInput"/>
        <button @click="handleSubmit">Save</button>
    </div>

    <div class="playerInputSaved" v-else> <!-- else: inputs are submitted, print the value (name) and corresponding symbols-->
        <p>{{ userOneInput }} [X] vs. {{ userTwoInput }} [O]</p>
    </div>

</template>

<!-- ********************************************************************************** -->

<style scoped>
.playerInput {
    display: flex;
    flex-direction: column;
    gap: 5px;
}

input {
    padding: 5px 10px;
    font-size: 1rem;
}
.playerInput button {
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

.playerInput button:hover {
    background-color: rgb(197, 21, 174);
    color: aliceblue;
    border: none;
}

p {
    font-size: 1.2rem;
    color: rgb(68, 68, 145);
    font-weight: 500;
}

</style>