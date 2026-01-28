<script setup>
import { ref } from 'vue'

const count = ref(0);
const step = ref(1)

function increment() {
    count.value += step.value
}

function decreament() {
    count.value -= step.value
}

function reset() {
    count.value = 0
}
</script>

<template>
    <div class="card">
        <h1>Counter App</h1>
        <p>Click buttons to change the number.</P>

        <div class="count"> {{ count }}</div>

        <div class="row">
            <button class="btn dec" @click="decreament">- Decrease</button>
            <button class="btn inc" @click="increment">+ Increase</button>
        </div>

        <div class="row">
            <button class="btn reset" @click="reset">Reset</button>
        </div>

        <div class="hint">
            Step: <input type="number" min="1" v-model.number="step">
        </div>
    </div>

</template>

<style scoped>
.card {
    width: min(480px, 92vw);
    background-color: white;
    border-radius: 16px;
    padding: 24px;
    box-shadow: 0 8px 30px rgba(0, 0, 0, 0.08);

}

h1{
    margin: 0  0 6px;
    text-align: center;
    font-size: 36px;
}
</style>