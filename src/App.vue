<script setup>

</script>

<template>
  <div class="app">
    <h2>Mini Game</h2>
    <button class="instructions-button">
      Show Instructions
    </button>
    <div class="game">
      <div
        class="player">
        <div class="arrow-box">
          <img src="./assets/arrow.png" alt="Arrow" class="arrow" />
        </div>
        <h2 class="player-title">
        </h2>
        <div class="scores">
          <p class="score-title">SCORE <span class="score total-score">{{ score }}</span></p>
          <p class="score-title">CURRENT <span class="score"></span></p>
        </div>
      </div>
    </div>
    <div class="controls">
      <div class="controls-buttons">
        <button class="button">
          <img src="./assets/play.png" alt="play" class="play-icon" />
          PLAY
        </button>
        <button class="button">
          <img src="./assets/pause.png" alt="pause" class="pause-icon" />
          PAUSE
        </button>
      </div>
      <button class="button">
        <img src="./assets/reset.png" alt="reset" class="reset-icon" />
        RESET
      </button>
      <button class="button">
        <img src="./assets/addPlayer.png" alt="add player" class="add-player-icon" />
        ADD PLAYER
      </button>
    </div>
    <div class="modal">
      <div class="modal-content">
        <img src="./assets/trophy.png" alt="trophy" class="trophy" />
        <p class="modal-text">Player {{ winner }} wins!</p>
        <button class="button close">CLOSE</button>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>