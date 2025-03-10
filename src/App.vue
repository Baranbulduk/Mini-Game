<script setup>
import { ref } from 'vue';
import redArrow from './assets/redArrow.png';
import blueArrow from './assets/blueArrow.png';
import yellowArrow from './assets/yellowArrow.png';

/* GlobalVariables */
const scores = ref([0, 0]);
const currentScore = ref(0);
const activePlayer = ref(0);
const playing = ref(true);
const showInstructions = ref(false);
const numPlayers = ref(2);
const showModal = ref(false);
const winner = ref(null);

const playerNames = ref(['Player 1', 'Player 2']);

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

/* Toggle Instructions */
function toggleInstructions() {
  showInstructions.value = !showInstructions.value;
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
    playerNames.value.push(`Player ${numPlayers.value}`);
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
    <div class="game">
      <div v-for="(score, index) in scores" :key="index"
        :class="['player', { 'player--active': activePlayer === index }]">
        <div class="arrow-box">
          <img v-if="activePlayer === index" :src="getArrowSrc(index)" alt="Arrow" class="arrow" />
        </div>
        <h2 :class="['player-title', { p1: index === 0, p2: index === 1, p3: index === 2 }]">{{ playerNames[index] }}
        </h2>
        <div class="scores">
          <p class="score-title">SCORE <span class="score total-score">{{ score }}</span></p>
          <p class="score-title">CURRENT <span class="score">{{ activePlayer === index ? currentScore : 0 }}</span></p>
        </div>
      </div>
    </div>
    <div class="controls">
      <div class="controls-buttons">
        <button class="button" @click="play">
          <img src="./assets/play.png" alt="play" class="play-icon" />
          PLAY
        </button>
        <button class="button" @click="pause">
          <img src="./assets/pause.png" alt="pause" class="pause-icon" />
          PAUSE
        </button>
      </div>
      <button class="button" @click="reset">
        <img src="./assets/reset.png" alt="reset" class="reset-icon" />
        RESET
      </button>
      <button class="button" @click="addPlayer" v-if="numPlayers < 3">
        <img src="./assets/addPlayer.png" alt="add player" class="add-player-icon" />
        ADD PLAYER
      </button>
    </div>
    <div v-if="showModal" class="modal" @click="closeModal">
      <div class="modal-content" @click.stop>

        <img src="./assets/trophy.png" alt="trophy" class="trophy" />
        <p class="modal-text">Player {{ winner }} wins!</p>
        <button class="button close" @click="closeModal">CLOSE</button>
      </div>
    </div>
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
  width: 1000px;
  border-radius: 20px;
}

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
  padding: 20px;
  width: 400px;
}

.highlight {
  color: #00af0f;
  font-weight: bold;
}

.game {
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 100%;
  margin-bottom: 50px;
}

.arrow-box {
  height: 35px;
}

.arrow {
  width: 40px;
  height: 40px;
  animation: arrow 2s ease-in-out infinite;
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
  color: #000;
}

.score {
  background-color: #f5f5f5;
  color: #000;
  font-size: 1.4rem;
  font-weight: bold;
  width: 100px;
  padding: 0px 10px;
  border-radius: 5px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.total-score {
  color: #00af0f;
}

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
  padding: 10px 20px;
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

.modal {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgba(0, 0, 0, 0.651);
}

.modal-content {
  background-color: #ffffff;
  padding: 5px 20px;
  height: 200px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 200px;
  border-radius: 10px;
}

.trophy {
  width: 50px;
  height: 50px;
}

.modal-text {
  color: #000000;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.4rem;
  font-weight: 700;
}

.close {
  background-color: #b90000;
  color: #ffffff;
  float: right;
  z-index: 2;
  font-size: 14px;
  padding: 5px 55px;
  margin-top: 40px;
  margin-bottom: -20px;
}

.close:hover,
.close:focus {
  background-color: #940000;
  color: rgb(255, 255, 255);
  box-shadow: none;
  cursor: pointer;
}
</style>