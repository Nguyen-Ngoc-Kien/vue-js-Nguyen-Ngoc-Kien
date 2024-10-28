
<script setup>
import { ref, computed } from 'vue';

const sideLength = ref(0);

const area = computed(() => sideLength.value ** 2);
</script>

<template>
    <div>
        <h1>Tính Diện Tích Hình Vuông</h1>
        <label for="sideLength">Nhập chiều dài cạnh:</label>
        <input type="number" v-model.number="sideLength" id="sideLength">
        <p>Diện tích của hình vuông là: {{ area }}</p>
    </div>    
</template>

<style lang="css" scoped>

</style>