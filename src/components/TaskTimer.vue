<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

let tasks = ref([
    { id: 1, title: '讀書', time: 0, isRunning: false },
    { id: 2, title: '運動', time: 0, isRunning: false }
])
let newTaskTitle = ref('');

const startTimer = (task) => {
    if(task.isRunning) return
    task.isRunning = true
    //計時器邏輯
    task.timeID = window.setInterval(() =>{
        task.time ++
    }, 1000)
}

const stopTimer = (task) => {
    task.isRunning = false
    //停止計時器邏輯
    window.clearInterval(task.timeID);
    task.timeID = null;
}

const deleteTask = (task) => {
    tasks.value = tasks.value.filter((item) => item != task)
}

const formatTime = (seconds) =>{
    const hr = String(Math.floor(seconds / 3600)).padStart(2, '0');
    const min = String(Math.floor((seconds % 3600) / 60)).padStart(2, '0');
    const sec = String(Math.floor(seconds % 60)).padStart(2, '0');
    return `${hr}:${min}:${sec}`
} 

const addTask = () =>{
    if(!newTaskTitle.value.trim()) return;
    // const preID = tasks.value.length ? tasks.value[tasks.value.length-1].id : 0;
    tasks.value.push({
        id: Date.now(),
        title: newTaskTitle.value,
        time: 0,
        isRunning: false
    });
    newTaskTitle.value = ''
}

onMounted(() => {
    //初始化邏輯
    //可以載localStorage
})

onUnmounted(() => {
    //清理計時器
    //可以把所有計時器放在一個物件中，一次清除所有timeID
})
</script>

<template>
    <div class="container">
        <h2>任務計時器</h2>
        <input type="text" placeholder="輸入新任務名稱" v-model="newTaskTitle">
        <button class="greenBtn" @click="addTask">新增任務</button>
        <!-- 任務列表 -->
        <div v-for="task in tasks" :key="task.id" class="task-item">
            <h3>{{ task.title }}</h3>
            <p>已花費時間：{{ formatTime(task.time) }}秒</p>

            <!-- 開始/停止按鈕 -->
            <button @click="task.isRunning ? stopTimer(task) : startTimer(task)" :class="task.isRunning ? 'yellowBtn' : 'greenBtn'">
                {{ task.isRunning ? '停止':'開始' }}
            </button>
            <button @click="deleteTask(task)" class="redBtn">刪除</button>
        </div>
    </div>
</template>

<style>
.task-item{
    margin: 20px 0;
    padding: 15px;
    border: 1px solid #cecdcd;
    position: relative;
    background-color: #f1f1f1;
    border-radius: 10px;
}
.greenBtn{
    margin-left: 10px;
    color: white;
    background-color: rgb(35, 181, 81);
}
.yellowBtn{
    color: black;
    background-color: #fff04d;
}
.redBtn{
    color: white;
    background-color: rgb(245, 126, 126);
    position: absolute;
    right: 10px;
    top: 10px;
}
input{
    font-size: 20px;
    line-height: 2rem;
    width: 70vh;
}
</style>