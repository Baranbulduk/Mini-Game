<script setup>
import { ref } from 'vue';

const showInstructions = ref(false);

function toggleInstructions() {
    showInstructions.value = !showInstructions.value;
}
</script>

<template>
    <div>
        <button class="instructions-button" @click="toggleInstructions"> <img src="../assets/gamerules.png" alt="gamerules" class="gamerules-icon" />
            GAME RULES
        </button>
        <div v-if="showInstructions">
            <div>
                <p class="instructions-text">If you get a 1, your turn ends and your current score resets to 0.<br>
                    Pause to add your current score to your total score and end your turn.<br>
                    First player to reach <span class="highlight">50</span> points wins.</p>
            </div>
        </div>
    </div>
</template>

<style scoped>
.instructions-button {
    font-size: 0.8rem;
    margin-top: 20px;
    padding: 15px 40px;
    font-weight: 500;
    background-color: #000000;
    border: none;
    border-radius: 10px;
    font-family: inherit;
    cursor: pointer;
}

.instructions-button:hover {
    background-color: #1a1a1a;
}

.gamerules-icon {
    width: 20px;
    height: 20px;
    margin-right: 5px;
    margin-bottom: -4px;
}

.instructions-text {
    color: #000000;
    background-color: #f5f5f5;
    border: solid 1px #f0f0f0;
    border-radius: 10px;
    font-size: 1rem;
    padding: 30px;
    width: 530px;
    letter-spacing: 0.1px;
    margin-top: -20px;
}

.highlight {
    color: #21a700;
    font-weight: bold;
}
</style>