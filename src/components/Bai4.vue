<script setup>
import { ref, watch, computed } from 'vue';

const number1 = ref(0);
const number2 = ref(0);

const sum = computed(() => number1.value + number2.value);
const difference = computed(() => number1.value - number2.value);
const product = computed(() => number1.value * number2.value);
const quotient = computed(() => {
    return number2.value !== 0 ? (number1.value / number2.value).toFixed(2) : 'Không thể chia cho 0';
});
</script>

<template>
    <div>
        <h1>Máy Tính Đơn Giản</h1>
        <label for="number1">Nhập số thứ nhất:</label>
        <input type="number" v-model.number="number1" id="number1" />

        <label for="number2">Nhập số thứ hai:</label>
        <input type="number" v-model.number="number2" id="number2" />

        <p>Tổng: {{ sum }}</p>
        <p>Hiệu: {{ difference }}</p>
        <p>Tích: {{ product }}</p>
        <p>Thương: {{ quotient }}</p>
    </div>
</template>

<style scoped>
label {
    display: block;
    margin-top: 10px;
}

input {
    margin-bottom: 10px;
}

</style>