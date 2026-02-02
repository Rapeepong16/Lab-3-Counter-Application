<script setup>
import { ref } from "vue";
import { computed } from "vue";

const count = ref(0);
const step = ref(1);
const previousCount = ref(null);

const min = 0;
const max = 100;

function saveHistory() {
  previousCount.value = count.value;
}

function increment() {
  if (count.value + step.value <= max) {
    saveHistory();
    count.value += step.value;
  } else {
    saveHistory();
    count.value = max;
  }
}

function decrement() {
  if (count.value - step.value >= min) {
    saveHistory();
    count.value -= step.value;
  } else {
    saveHistory();
    count.value = min;
  }
}

function reset() {
  saveHistory();
  count.value = 0;
}

function undo() {
  if (previousCount.value !== null) {
    count.value = previousCount.value;
    previousCount.value = null;
  }
}

const canUndo = computed(() => previousCount.value !== null);
const isMin = computed(() => count.value <= min);
const isMax = computed(() => count.value >= max);
</script>

<template>
  <div class="card">
    <h1>Counter App</h1>
    <p class="subtitle">Click buttons to change the number.</p>

    <div class="count">{{ count }}</div>

    <div class="row">
      <button class="btn dec" @click="decrement" :disabled="isMin">
        - Decrease
      </button>

      <button class="btn inc" @click="increment" :disabled="isMax">
        + Increase
      </button>
    </div>

    <div class="row">
      <button class="btn reset" @click="reset">Reset</button>
      <button class="btn undo" @click="undo" :disabled="!canUndo">Undo</button>
    </div>

    <div class="hint">
      Step: <input type="number" min="1" v-model.number="step" />
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
  text-align: center;
  font-family: sans-serif;
  margin: 20px auto;
}

h1 {
  margin: 0 0 6px;
  font-size: 32px;
  color: #333;
}

.subtitle {
  color: #666;
  margin-bottom: 20px;
}

.count {
  font-size: 64px;
  font-weight: bold;
  margin: 20px 0;
  color: #2c3e50;
}

.row {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-bottom: 10px;
}

.btn {
  padding: 10px 20px;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  cursor: pointer;
  transition: 0.2s;
  font-weight: bold;
}

.btn:disabled {
  background-color: #ddd;
  color: #999;
  cursor: not-allowed;
}

.btn.inc {
  background-color: #4ade80;
  color: white;
}
.btn.inc:hover:not(:disabled) {
  background-color: #22c55e;
}

.btn.dec {
  background-color: #f87171;
  color: white;
}
.btn.dec:hover:not(:disabled) {
  background-color: #ef4444;
}

.btn.reset {
  background-color: #e5e7eb;
  color: #374151;
  width: 100px;
}
.btn.undo {
  background-color: #fbbf24;
  color: white;
  width: 100px;
}

.hint {
  margin-top: 20px;
  color: #666;
}

input[type="number"] {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  width: 60px;
  text-align: center;
  margin-left: 5px;
}
</style>
