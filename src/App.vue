<template>
    <h1 v-if="tasks.length > 0">
        You have {{tasks.length}} tasks to complete
    </h1>
    <h1 v-else>
        Please enter a task and time to begin
    </h1>

    <button @click="resetTimer">Reset</button>
    <button @click="stopTimer">Stop</button>
    <button @click="startTimer">Start</button>

    <input v-model="task" placeholder="Set Task">
    <input v-model="time" placeholder="Set Time">

    <button @click="addTodo">Add Todo</button>
    <p v-if="tryAgain">please enter a time and task</p>

    <h1 v-if="timer > 0">
        {{timer}} seconds remaining to complete {{currentTask.task}}
    </h1>
    <h1 v-else>
        Begin a task
    </h1>
    <ul>
        <li v-for="todo in tasks" :key="todo.time">
            <div v-if="todo.timer > 0">
                <h2>
                    {{todo.timer}} Seconds to : {{todo.task}}
                </h2>
                <button @click="removeTodo(todo)">X</button>
                <button @click="startTask(todo)">Begin Task</button>
            </div>
        </li>
    </ul>
</template>

<script>
export default {
    data() {
        return {
            timer: 0,
            id: '',
            task: '',
            tasks: [],
            currentTask: {},
            hasStarted: false,
            tryAgain: false,
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
            this.tryAgain = false;
            if (this.time && this.task) {
                this.tasks.push({ timer: this.time, task: this.task, done: false });
                this.task = '';
                this.time = '';
            } else {
                this.tryAgain = true;
            }
        },
        removeTodo(task) {
            this.tasks = this.tasks.filter((t) => t !== task);
        },
        resetTimer() {
            window.location.reload();
        },
        startTimer() {  
            this.stopTimer();
            this.id = setInterval(() => this.countdownTime(), 1000);
        },
        stopTimer() {
            clearInterval(this.id);
        },
        countdownTime() {
            if (this.timer > 0)
                this.timer--;
        },
        setTime() {
            this.stopTimer();
            this.timer = this.updateTimer;
        }
    },
}
</script>
