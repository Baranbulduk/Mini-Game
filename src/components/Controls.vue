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
            <button class="button reset" @click="reset">
                <img src="../assets/reset.png" alt="reset" class="reset-icon" />
                RESET
            </button>
            <button class="button play-pause" @click="play">
                <img src="../assets/play.png" alt="play" class="play-icon" />
                PLAY
            </button>
            <button class="button play-pause" @click="pause">
                <img src="../assets/pause.png" alt="pause" class="pause-icon" />
                PAUSE
            </button>
            <button class="button addplayer" @click="addPlayer" v-if="props.numPlayers < 3">
                <img src="../assets/addPlayer.png" alt="add player" class="add-player-icon" />
                ADD PLAYER
            </button>
        </div>
    </div>
</template>

<style scoped>
.controls {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    gap: 10px;
    margin-top: 50px;
    width: 900px;
}

.controls-buttons {
    display: flex;
    justify-content: space-between;
    gap: 10px;
}

.button {
    padding: 20px;
    font-size: 0.8rem;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #000000;
    color: #ffffff;
    border: none;
    border-radius: 10px;
    font-weight: 700;
    font-family: inherit;
    width: 210px;
}

.button:hover {
    background-color: #272727;
}

.reset {
    background-color: #a50000;
    color: #ffffff;
}

.reset:hover {
    background-color: #770000;
}

.play-icon {
    width: 30px;
    height: 30px;
    margin-right: 6px;
}

.pause-icon {
    width: 28px;
    height: 28px;
    margin-right: 6px;
}

.reset-icon {
    width: 26px;
    height: 26px;
    margin-right: 8px;
}

.add-player-icon {
    width: 26px;
    height: 26px;
    margin-right: 8px;
}

@media screen and (max-width: 1300px) {
    .controls-buttons {
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
        gap: 40px;
    }

    .button {
        padding: 15px;
        font-size: 2.5rem;
        height: 150px;
        width: 1000px;
    }

    .play-icon {
        width: 50px;
        height: 50px;
        margin-right: 18px;
    }

    .pause-icon {
        width: 48px;
        height: 48px;
        margin-right: 18px;
    }

    .reset-icon {
        width: 46px;
        height: 46px;
        margin-right: 20px;
    }

    .add-player-icon {
        width: 46px;
        height: 46px;
        margin-right: 20px;
    }
}
</style>