<script setup>
import { defineEmits, defineProps } from 'vue';

/* Props */
const props = defineProps({
    numPlayers: Number
});

/* Emits */
const emit = defineEmits(['play', 'pause', 'reset', 'addPlayer']);

/* Play */
function play() {
    emit('play');
}

/* Pause */
function pause() {
    emit('pause');
}

/* Reset */
function reset() {
    emit('reset');
}

/* Add Player */
function addPlayer() {
    emit('addPlayer');
}
</script>

<template>
    <div class="controls">
        <div class="controls-buttons">
            <button class="button" @click="play">
                <img src="../assets/play.png" alt="play" class="play-icon" />
                PLAY
            </button>
            <button class="button" @click="pause">
                <img src="../assets/pause.png" alt="pause" class="pause-icon" />
                PAUSE
            </button>
        </div>
        <button class="button" @click="addPlayer" v-if="props.numPlayers < 3">
            <img src="../assets/addPlayer.png" alt="add player" class="add-player-icon" />
            ADD PLAYER
        </button>
        <button class="button" @click="reset">
            <img src="../assets/reset.png" alt="reset" class="reset-icon" />
            RESET
        </button>

    </div>
</template>

<style scoped>
.controls {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    gap: 10px;
    margin-top: 20px;
}

.controls-buttons {
    display: flex;
    justify-content: space-around;
    gap: 10px;
}

.button {
    padding: 15px 40px;
    font-size: 0.8rem;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #000000;
    border: none;
    border-radius: 10px;
    font-weight: 500;
    font-family: inherit;
}

.button:hover {
    background-color: #313131;
}

.button-icon {
    width: 20px;
    height: 20px;
    padding-right: 6px;
    margin-bottom: -2px;
}

.play-icon {
    width: 18px;
    height: 18px;
    margin-right: 6px;
    margin-top: 1px;
}

.pause-icon {
    width: 16px;
    height: 16px;
    margin-right: 6px;
    margin-top: 1px;
}

.reset-icon {
    width: 14px;
    height: 14px;
    margin-right: 8px;
    margin-top: 2px;
}

.add-player-icon {
    width: 14px;
    height: 14px;
    margin-right: 8px;
    margin-top: 1px;
}
</style>