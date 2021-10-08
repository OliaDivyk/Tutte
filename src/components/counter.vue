<template>
    <div class="counter">
        <div class="stopwatch">      
            <p>{{ time | secondsInMinutes }}</p>
            <div class="control-button">
                <span class="button" @click="start">Start</span>
                <span class="button" @click="stop">Stop</span>
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
            time: 0,
            timerStatus: null
        }
    },
    mounted() {
        this.startTimer()
    },
    methods: {
        startTimer: function() {
            this.resetTime()
            this.timerStatus = setInterval(() => {
                this.time++
            }, 1000)
        },
        start: function() {
            clearInterval(this.timerStatus)
            this.startTimer()
        },
        stop: function() {
            clearInterval(this.timerStatus)
        },
        resetTime: function() {
            return this.time = 0
        }
    },
    filters: {
        secondsInMinutes: function(seconds) {
            return moment("2015-01-01")
                .startOf("day")
                .seconds(seconds)
                .format("HH:mm:ss");
        }
    },
    destroyed() {
        this.resetTime()
    }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto+Mono:wght@300&display=swap');
body {
    background: #333333;
}
p {
    font-family: 'Roboto Mono', monospace;
    color: #fff8e4;
    font-size: 64px;    
}
.counter {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100vw;
    height: 100vh;
}
.control-button {
    display: flex;
    justify-content: space-between;
}
.control-button .button {
    color: #a19e96;
    font-size: 36px;
}
.control-button .button:hover {
    color: #fff8e4;
    cursor: pointer;
    transition: ease-in-out(.3s);
}
</style>