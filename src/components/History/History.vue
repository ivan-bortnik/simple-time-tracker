<template>
    <div id="root">

        <h1>History</h1>

        <div class="container">
            <ul>
                <li v-for="(item, key) in $parent.history" :key="key">
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
        }
    }
}
</script>

<style scoped src="./History.css"></style>