<script setup>
import { ref, computed } from 'vue';

const isChecked = ref(false);

const textStyle = computed(() => {
    return {
        color: isChecked.value ? 'blue' : 'red',
        fontWeight: isChecked.value ? 'bold' : 'normal'
    };
});
</script>

<template>
    <div>
        <h1>Thay Đổi Kiểu Chữ Dựa Trên Checkbox</h1>
        <label>
            <input type="checkbox" v-model="isChecked" />
            Chọn để đổi màu và kiểu chữ
        </label>
        
        <p :style="textStyle">Đoạn văn bản này sẽ thay đổi màu sắc và kiểu chữ!</p>
    </div>
</template>

<style scoped>
label {
    margin-bottom: 10px;
    display: block;
}
p {
    transition: color 0.3s, font-weight 0.3s; /* Thêm hiệu ứng chuyển tiếp */
}
</style>