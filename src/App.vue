<script setup>
import { ref } from 'vue';
import redArrow from './assets/redArrow.png';
import blueArrow from './assets/blueArrow.png';
import yellowArrow from './assets/yellowArrow.png';
import Instructions from './components/Instructions.vue';
import Player from './components/Player.vue';
import Controls from './components/Controls.vue';
import Modal from './components/Modal.vue';

/* GlobalVariables */
const scores = ref([0, 0]);
const currentScore = ref(0);
const activePlayer = ref(0);
const playing = ref(true);
const numPlayers = ref(2);
const showModal = ref(false);
const winner = ref(null);

const playerNames = ref(['PLAYER 1', 'PLAYER 2']);

/* Get Arrow Images */
function getArrowSrc(index) {
  if (index === 0) {
    return redArrow;
  } else if (index === 1) {
    return blueArrow;
  } else if (index === 2) {
    return yellowArrow;
  }
}

/* Play */
function play() {
  if (playing.value) {
    const playNumber = Math.trunc(Math.random() * 5) + 1;

    if (playNumber !== 1) {
      currentScore.value += playNumber;
    } else {
      switchPlayer();
    }
  }
}

/* Pause */
function pause() {
  if (playing.value) {
    scores.value[activePlayer.value] += currentScore.value;

    if (scores.value[activePlayer.value] >= 50) {
      playing.value = false;
      winner.value = activePlayer.value + 1;
      showModal.value = true;
      reset();
    } else {
      switchPlayer();
    }
  }
}

/* Reset */
function reset() {
  scores.value = Array(numPlayers.value).fill(0);
  currentScore.value = 0;
  activePlayer.value = 0;
  playing.value = true;
}

/* Add Player */
function addPlayer() {
  if (numPlayers.value < 3) {
    numPlayers.value += 1;
    scores.value.push(0);
    playerNames.value.push(`PLAYER ${numPlayers.value}`);
  }
}

/* Switch Player */
function switchPlayer() {
  currentScore.value = 0;
  activePlayer.value = (activePlayer.value + 1) % numPlayers.value;
}

/* Modal */
function closeModal() {
  showModal.value = false;
}
</script>

<template>
  <div class="app">
    <h1>Mini Game</h1>
    <Instructions />
    <div class="game">
      <Player v-for="(score, index) in scores" :key="index" :playerName="playerNames[index]" :score="score"
        :currentScore="activePlayer === index ? currentScore : 0" :isActive="activePlayer === index"
        :arrowSrc="getArrowSrc(index)" :playerClass="index === 0 ? 'p1' : index === 1 ? 'p2' : 'p3'" />
    </div>
    <Controls :numPlayers="numPlayers" @play="play" @pause="pause" @reset="reset" @addPlayer="addPlayer" />
    <Modal :showModal="showModal" :winner="winner" @closeModal="closeModal" />
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
}

.app {
  background-color: rgb(255, 255, 255);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 50px 0;
  width: 1200px;
  height: 700px;
  border-radius: 20px;
}

.game {
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 100%;
  margin-bottom: 50px;
}
</style>