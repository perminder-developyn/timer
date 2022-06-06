<template>
    <br>
        Countdown Timer : {{timer}} SECONDS
    <br>
        <input v-model="updateTimer" placeholder="Set Time"><br>
        <button @click="setTime">Set</button><br>
        <button @click="startTimer">Start</button><br>
        <button @click="resetTimer">Reset</button><br>
        <button @click="stopTimer">Stop</button>
    <br>
    <br>
        Timed Tasks
        <form @submit.prevent="addTodo">
            <input v-model="task" placeholder="Set Task">
            <input v-model="time" placeholder="Set Time">
            <button>Add Todo</button>
        </form>
    <ul>
        <p v-if="hasStarted">
            {{timer}} seconds remaining to complete {{currentTask.task}}
        </p>
    <li v-for="todo in tasks" :key="todo.time">
        {{todo.timer}} Seconds to : {{ todo.task}}
        <button @click="removeTodo(todo)">X</button>
        <button @click="startTask(todo)">Begin Task</button>
    </li>
    </ul>
</template>

<script>
export default {
    data() {
        return {
        timer: 60,
        updateTimer: null,
        id: "",
        task: '',
        tasks: [],
        currentTask: {},
        hasStarted: false
        }
    },
    methods: {
    startTask(task) {
        this.currentTask = task;
        this.hasStarted = true;
        this.timer = this.currentTask.timer;
        this.startTimer();
    },
    addTodo() {
        this.tasks.push({ timer: this.time, task: this.task, done: false });
        this.task="";
        this.time = "";
    },
    removeTodo(task) {
        this.tasks = this.tasks.filter((t) => t !== task);
    },
    resetTimer() {
        window.location.reload();
    },
    startTimer() {  
        clearInterval(this.id)
        this.id = setInterval(() => this.countdownTime(), 1000);
    },
    stopTimer() {
        clearInterval(this.id);
    },
    countdownTime() {
        if (this.timer > 0)
        this.timer--;
    },
    setTime(){
        this.stopTimer();
        this.timer = this.updateTimer;
    }
    },
    watch: {
        updateTimer(value) {
            console.log(value);
        } 
    }

}
</script>


<style>

</style>
