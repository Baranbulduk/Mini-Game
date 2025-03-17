<script setup>
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
    showModal: Boolean,
    winner: Number
});

const emit = defineEmits(['closeModal']);

function closeModal() {
    emit('closeModal');
}
</script>

<template>
    <div v-if="showModal" class="modal" @click="closeModal">
        <div class="modal-content" @click.stop>
            <img src="../assets/trophy.png" alt="trophy" class="trophy" />
            <p class="modal-text">Player {{ winner }} wins!</p>
            <button class="button close" @click="closeModal">CLOSE</button>
        </div>
    </div>
</template>

<style scoped>
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
    padding: 20px;
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

.button {
    padding: 10px 20px;
    font-size: 0.8rem;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    border: none;
    border-radius: 10px;
    font-weight: 500;
    font-family: inherit;
}


.close {
    background-color: #b90000;
    color: #ffffff;
    float: right;
    z-index: 2;
    font-size: 14px;
    padding: 5px 55px;
    margin-top: 40px;
}

.close:hover,
.close:focus {
    background-color: #940000;
    color: rgb(255, 255, 255);
    box-shadow: none;
    cursor: pointer;
}
</style>