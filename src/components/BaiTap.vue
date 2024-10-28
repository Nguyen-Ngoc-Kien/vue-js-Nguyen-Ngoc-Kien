<template>
  <div class="app-container">
    <h1>Quản Lý Công Việc</h1>
    <form @submit.prevent="addTask" class="task-form">
      <label>Tên Công Việc</label>
      <input v-model="newTaskName" placeholder="Tên công việc" required />

      <label>Thời gian dự kiến</label>
      <div class="estimated-time-input">

        <input v-model="newTaskEstimatedTime" type="number" min="1" placeholder="Thời gian dự kiến" required />
        <select v-model="newTaskTimeUnit">
          <option value="seconds">Giây</option>
          <option value="minutes">Phút</option>
          <option value="hours">Giờ</option>
          <option value="days">Ngày</option>
        </select>
      </div>

      <button type="submit">Thêm Công Việc</button>
    </form>

    <div class="tasks">
      <h2>Danh Sách Công Việc</h2>
      <ul>
        <li v-for="(task, index) in tasks" :key="index" :class="{ completed: task.status === 'Hoàn thành', overdue: task.status === 'Quá hạn' }">
          <p><strong>{{ task.name }}</strong></p>
          <p>Thời gian khởi tạo: {{ task.createdAt.toLocaleString('vi-VN') }}</p>
          <p>Thời gian dự kiến: {{ task.estimatedTime }} {{ task.timeUnit }}</p>
          <p>Trạng thái: {{ task.status }}</p>
          <p v-if="task.status === 'Hoàn thành' || task.status === 'Quá hạn'">Thời gian hoàn thành: {{ task.completedAt }}</p>
          <button @click="toggleStatus(task)">Đánh dấu là {{ task.status === 'Hoàn thành' ? 'Chưa hoàn thành' : 'Hoàn thành' }}</button>
        </li>
      </ul>
    </div>

    <p class="completed-count">Số lượng công việc đã hoàn thành: {{ completedTasksCount }}</p>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const tasks = ref([]);

const newTaskName = ref('');
const newTaskEstimatedTime = ref(0);
const newTaskTimeUnit = ref('hours'); 

const addTask = () => {
  tasks.value.push({
    name: newTaskName.value,
    estimatedTime: Number(newTaskEstimatedTime.value), 
    timeUnit: newTaskTimeUnit.value, 
    status: 'Chưa hoàn thành',
    completedAt: null,
    createdAt: new Date() 
  });
  newTaskName.value = '';
  newTaskEstimatedTime.value = 0;
  newTaskTimeUnit.value = 'hours';
};

const toggleStatus = (task) => {
  if (task.status === 'Chưa hoàn thành') {
    const now = new Date();
    task.completedAt = now.toLocaleString('vi-VN'); 
    const elapsedTime = (now - task.createdAt) / 1000;

    let estimatedTimeInSeconds;
    switch (task.timeUnit) {
      case 'seconds':
        estimatedTimeInSeconds = task.estimatedTime;
        break;
      case 'minutes':
        estimatedTimeInSeconds = task.estimatedTime * 60;
        break;
      case 'hours':
        estimatedTimeInSeconds = task.estimatedTime * 60 * 60;
        break;
      case 'days':
        estimatedTimeInSeconds = task.estimatedTime * 24 * 60 * 60;
        break;
      default:
        estimatedTimeInSeconds = task.estimatedTime * 60 * 60;
    }

    task.status = elapsedTime > estimatedTimeInSeconds ? 'Quá hạn' : 'Hoàn thành';
  } else {
    task.status = 'Chưa hoàn thành';
    task.completedAt = null;
  }
};

const completedTasksCount = computed(() => tasks.value.filter(task => task.status === 'Hoàn thành').length);

</script>

<style scoped>
.app-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.task-form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 20px;
}

.estimated-time-input {
  display: flex;
  gap: 5px;
}

.tasks ul {
  list-style: none;
  padding: 0;
}

.tasks li {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
  margin-bottom: 10px;
  background-color: #f9f9f9;
}

.tasks li.completed {
  background-color: #d4edda;
  color: #155724;
}

.tasks li.overdue {
  background-color: #f8d7da;
  color: #721c24;
}

button {
  padding: 5px 10px;
  font-size: 14px;
  cursor: pointer;
}

.completed-count {
  font-weight: bold;
  margin-top: 20px;
  text-align: center;
}
</style>