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
        <input type="text" placeholder="Player 1" v-model="userOneInput"/>
        <input type="text" placeholder="Player 2" v-model="userTwoInput"/>
        <button @click="handleSubmit">Save</button>
    </div>

    <div v-else> <!-- else: inputs are submitted, print the value (name) and corresponding symbols-->
        <p>{{ userOneInput }} = X</p>
        <p>{{ userTwoInput }} = O</p>
    </div>

</template>

<!-- ********************************************************************************** -->

<style scoped>
.playerInput {
    display: flex;
    flex-direction: column;
    gap: 5px;
}

.playerInput button {
    padding: 5px;
    width: 30%;
    align-self: center;
    text-align: center;
    margin: 10px;
}
</style>