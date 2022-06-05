<template>
<input v-model="updateTimer">
<button @click="setTime">Set</button>
<button @click="startTimer">Start</button>
<button @click="resetTimer">Reset</button>
<button @click="stopTimer">Stop</button>
{{timer}}
</template>

<script>
export default{
    data(){
        return{
        timer: 60,
        updateTimer: null,
        id: ""
    }
    },
    methods:{
    resetTimer(){
        window.location.reload()
    },
    startTimer(){  
      this.id = setInterval(() => this.countdownTime(), 1000);
    },
    stopTimer(){
        clearInterval(this.id)
    },
    countdownTime(){
        if(this.timer > 0)
        this.timer--;
    },
    setTime(){
        this.stopTimer()
        this.timer = this.updateTimer
    }
    },
    watch: {
        updateTimer(value){
            console.log(value)
        } 
    }

}
</script>


<style>

</style>
