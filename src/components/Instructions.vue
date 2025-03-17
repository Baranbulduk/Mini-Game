<script setup>
import { ref } from 'vue';

const showInstructions = ref(false);

function toggleInstructions() {
    showInstructions.value = !showInstructions.value;
}
</script>

<template>
    <div>
        <button class="instructions-button" @click="toggleInstructions">
            GAME RULES
        </button>
        <div v-if="showInstructions">
            <div>
                <p class="instructions-text">If you get a 1, your turn ends and your current score resets to 0.<br>
                    Hold to add your current score to your total score and end your turn.<br>
                    First player to reach <span class="highlight">50</span> points wins.</p>
            </div>
        </div>
    </div>
</template>

<style scoped>
.instructions-button {
    font-size: 0.8rem;
    margin-top: 20px;
    padding: 10px 20px;
    font-weight: 500;
    background-color: #000000;
    border: none;
    border-radius: 10px;
    font-family: inherit;
    cursor: pointer;
}

.instructions-button:hover {
    background-color: #313131;
}

.instructions-text {
    color: #000000;
    background-color: #f5f5f5;
    border-radius: 10px;
    font-size: 0.8rem;
    padding: 30px;
    width: 450px;
    letter-spacing: 0.5px;
    margin-top: -15px;
}

.highlight {
    color: #00af0f;
    font-weight: bold;
}
</style>