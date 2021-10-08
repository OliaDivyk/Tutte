<template>
<div class="counter vh-100 vw-100">
    <div class="stopwatch">      
        <p>{{ time | secondsInMinutes }}</p>
        <div class="control-button">
            <span @click="start">Start</span>
            <span @click="stop">Stop</span>
        </div>
    </div>
</div>
</template>

<script>
import moment from 'moment'

export default {
    name: 'counter',
    data() {
        return {
            timerWorking: false,
            time: 0,
            timerStatus: null
        }
    },
    mounted() {
        this.timerWorking = true
        this.start()
    },
    methods: {
        start: function() {
            this.time = 0
            this.timerStatus = setInterval(() => {
                this.time++
            }, 1000)
        },
        stop: function() {
            clearInterval(this.timerStatus)
        }
    },
    filters: {
        secondsInMinutes: function(seconds) {
            return moment("2015-01-01")
                .startOf("day")
                .seconds(seconds)
                .format("HH:mm:ss");
        }
    }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto+Mono:wght@300&display=swap');

p {
    font-family: 'Roboto Mono', monospace;
    color: #fff8e4;
    font-size: 64px;    
}
.counter {
    background: #333333;
    display: flex;
    justify-content: center;
    align-items: center;
}
.control-button {
    display: flex;
    justify-content: space-between;
}
.control-button span {
    color: #a19e96;
    font-size: 36px;
}
.control-button span:hover {
    color: #fff8e4;
    cursor: pointer;
    transition: ease-in-out(.3s);
}
</style>