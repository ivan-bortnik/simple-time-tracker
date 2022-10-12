<template>
    <div id="root">

        <stop-confirmation v-if="needConfirmation"></stop-confirmation>

        <div class="current-task">
            <p style="font-weight: light; opacity: .6">Working on</p>
            <p style="font-weight: bold;">{{ workingon }}</p>
        </div>

        <p id="timer">{{ formatTime() }}</p>

        <div class="control-buttons">
            <img :src="buttonSource" @click="toggleTimer" class="btn">
            <img src="../../assets/btn_stop.png" @click="stop" class="btn">
        </div>

    </div>    
</template>

<script>

import StopConfirmation from '../StopConfirmation/StopConfirmation.vue';

export default {
    name: "Timer",

    props: ["workingon"],

    components: {
        'stop-confirmation': StopConfirmation
    },

    data () {
        return {

            elapsedTime: 0,
            isRunning: false,
            timer: 0,
            buttonSource: require('../../assets/btn_start.png'),

            buttonStart: require('../../assets/btn_start.png'),
            buttnPause: require('../../assets/btn_pause.png'),

            needConfirmation: false

        }
    },

    methods: {

        toggleTimer () {
            if (this.isRunning) {
                this.pause();
                this.buttonSource = this.buttonStart;
            } else {
                this.start();
                this.buttonSource = this.buttnPause
            }
        },

        start () {
            this.isRunning = true;

            this.timer = setInterval(() => {
                this.elapsedTime++;
            }, 1000);
        },

        pause () {
            clearInterval(this.timer);
            this.isRunning = false;
        },

        stop () {
            this.needConfirmation = true;
            this.pause();
        },

        resetTimer () {
            clearInterval(this.timer);
            this.isRunning = false;
            this.buttonSource = this.buttonStart;
            
            this.$parent.saveToHistory(this.elapsedTime);
            
            // bro...
            this.$parent.projects[this.$parent.currentTask.project].tasks[this.$parent.currentTask.task].elapsedTime += this.elapsedTime;
            this.elapsedTime = 0;


            // Save
            this.$parent.save();
        },

        formatTime () {
            // Return elapsed time in a string in a HH:MM:SS format
            let hrs = `${Math.floor(this.elapsedTime / 3600)}`.padStart(2, '0');
            let min = `${Math.floor(this.elapsedTime % 3600 / 60)}`.padStart(2, '0');
            let sec = `${this.elapsedTime % 60}`.padStart(2, '0');

            return `${hrs}:${min}:${sec}`;
        }

    }   
}
</script>

<style scoped src="./Timer.css">



</style>