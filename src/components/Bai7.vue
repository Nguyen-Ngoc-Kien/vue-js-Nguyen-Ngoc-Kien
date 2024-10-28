<script setup>
import { ref, computed, watch } from 'vue';

const fullName = ref('');
const email = ref('');
const phone = ref('');
const password = ref('');
const rePassword = ref('');

const isButtonDisabled = computed(() => {
    return password.value.length < 8 || !isFormFilled.value;
});

const buttonClass = computed(() => {
    return {
        'btn-active': password.value.length >= 8 && isFormFilled.value,
        'btn-disabled': password.value.length < 8 || !isFormFilled.value,
    };
});

const isFormFilled = computed(() => {
    return fullName.value && email.value && phone.value && password.value && rePassword.value;
});

const formCompleted = ref(false);
const completionMessage = 'Form đã hoàn tất!';

const handleSubmit = () => {
    formCompleted.value = true;
};
</script>

<template>
    <div class="container">
        <h1>Đăng Ký Tài Khoản</h1>
        <form @submit.prevent="handleSubmit" class="form">
            <div class="form-group">
                <label for="fullName">Họ Tên:</label>
                <input type="text" v-model="fullName" id="fullName" required placeholder="Nhập họ tên" />
            </div>
            <div class="form-group">
                <label for="email">Email:</label>
                <input type="email" v-model="email" id="email" required placeholder="Nhập email" />
            </div>
            <div class="form-group">
                <label for="phone">Số Điện Thoại:</label>
                <input type="tel" v-model="phone" id="phone" required placeholder="Nhập số điện thoại" />
            </div>
            <div class="form-group">
                <label for="password">Mật Khẩu:</label>
                <input type="password" v-model="password" id="password" required placeholder="Nhập mật khẩu" />
            </div>
            <div class="form-group">
                <label for="rePassword">Nhập Lại Mật Khẩu:</label>
                <input type="password" v-model="rePassword" id="rePassword" required placeholder="Nhập lại mật khẩu" />
            </div>
            <button :class="buttonClass" :disabled="isButtonDisabled">Đăng Ký</button>
        </form>
        <p v-if="formCompleted" class="completion-message">{{ completionMessage }}</p>
    </div>
</template>

<style scoped>
.container {
    max-width: 400px;
    margin: 50px auto;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    background-color: #f9f9f9;
}

h1 {
    text-align: center;
    margin-bottom: 20px;
}

.form {
    display: flex;
    flex-direction: column;
}

.form-group {
    margin-bottom: 15px;
}

label {
    margin-bottom: 5px;
    font-weight: bold;
}

input {
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    transition: border-color 0.3s;
    font-size: 16px;
}

input:focus {
    border-color: #007bff;
    outline: none;
}

.btn-active {
    background-color: #007bff;
    color: white;
    border: none;
    padding: 10px;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
}

.btn-disabled {
    background-color: gray;
    color: white;
    border: none;
    padding: 10px;
    border-radius: 5px;
    cursor: not-allowed;
}

.btn-active:hover {
    background-color: #0056b3;
}

.completion-message {
    text-align: center;
    margin-top: 20px;
    color: green;
    font-weight: bold;
}
</style>