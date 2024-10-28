<script setup>
import { ref } from 'vue';

const fontSize = ref(16); 
</script>

<template>
    <div>
        <h1>Thay Đổi Kích Thước Chữ</h1>
        <label for="fontSize">Nhập kích thước chữ (px):</label>
        <input type="number" v-model.number="fontSize" id="fontSize" placeholder="Nhập kích thước chữ">
        <p class="text" v-bind:style="{ fontSize: fontSize + 'px' }">Đoạn văn bản với kích thước chữ đã cập nhật.</p>
    </div>
</template>

<style scoped>
.text {
    transition: font-size 0.3s;
}
</style>