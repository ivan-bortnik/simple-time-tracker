<template>
    <div id="root">

        <h1>History</h1>

        <div class="container">
            <ul>
                <li v-for="(item, key) in $parent.history" :key="key"
                :style="{'border-color': getColor(item.colorTag)}"
                @click="setTask(item.projectID, item.taskID)">
                    <span class="name">{{ item.name }}</span>
                    <br>
                    <span class="time">{{ formatTime(item.elapsedTime) }}</span>
                    <span class="date">{{ item.date }}</span>
                </li>
            </ul>
        </div>

    </div>
</template>

<script>
export default {
    methods: {
        formatTime (time) {
            // Return elapsed time in a string in a HH:MM:SS format
            let hrs = `${Math.floor(time / 3600)}`.padStart(2, '0');
            let min = `${Math.floor(time % 3600 / 60)}`.padStart(2, '0');
            let sec = `${time % 60}`.padStart(2, '0');

            return `${hrs}:${min}:${sec}`;
        },

        getColor (tagID) {
            // Simply returns the hex value from the premade pallete
            // Colors are RED; GREEN; BLUE; PURPLE; YELLOW; WHITE
            return ["#b52616", "#46b516", "#1650b5", "#a10e97", "#e8c70c", "#ffffff"][tagID];
        },

        setTask (projectIdx, taskIdx) {
            this.$parent.currentTask = { project: projectIdx, task: taskIdx };
            this.$parent.currentTab = 'timer';
        }
    }
}
</script>

<style scoped src="./History.css"></style>