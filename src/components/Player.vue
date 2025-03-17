<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    playerName: String,
    score: Number,
    currentScore: Number,
    isActive: Boolean,
    arrowSrc: String,
    playerClass: String
});
</script>

<template>
    <div :class="['player', { 'player--active': isActive }]">
        <div class="arrow-box">
            <img v-if="isActive" :src="arrowSrc" alt="Arrow" class="arrow" />
        </div>
        <h2 :class="['player-title', playerClass]">{{ playerName }}</h2>
        <div class="scores">
            <p class="score-title">SCORE</p>
            <p> <span class="score total-score">{{ score }}</span></p>
            <p class="score-title">CURRENT</p>
            <p> <span class="score">{{ currentScore }}</span></p>
        </div>
    </div>
</template>

<style scoped>
.arrow-box {
    height: 35px;
    margin-top: 10px;
}

.arrow {
    width: 40px;
    height: 40px;
    animation: arrow 1s ease-in-out infinite;
}

@keyframes arrow {
    0% {
        transform: translateY(0);
    }

    50% {
        transform: translateY(-10px);
    }

    100% {
        transform: translateY(0);
    }
}

.player-title {
    font-size: 1.6rem;
    font-weight: 1000;
    margin-top: 0px;
    margin-bottom: 10px;
}

.p1 {
    color: #b90000;
}

.p2 {
    color: #0f00dd;
}

.p3 {
    color: #d8d402;
}

.scores {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 10px;
}

.score-title {
    font-size: 0.8rem;
    font-weight: bold;
    margin-top: 5px;
    margin-bottom: -35px;
    padding: 0px 10px;
    border-radius: 5px;
    color: #000000;
    background-color: #ffffff;
    z-index: 1;
}

.score {
    background-color: #f5f5f5;
    color: #000;
    font-size: 30px;
    font-weight: bold;
    width: 100px;
    padding: 5px 10px;
    border-radius: 5px;
    display: flex;
    align-items: center;
    justify-content: center;
    border: solid 1px #f0f0f0;
    margin-bottom: -20px;
}

.total-score {
    color: #00af0f;
}
</style>