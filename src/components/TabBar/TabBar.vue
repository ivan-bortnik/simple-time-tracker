<template>
    <div id="root">

        <button class="tab"
        :style="[selectedTab == 'projects'?{'background-color':'#25261D'}:{'background-color':'#0A0E08'}]"
        @click="$parent.currentTab = 'projects'; selectedTab = 'projects'"><img src="../../assets/list.png" alt=""></button>

        <button class="tab"
        :style="[selectedTab == 'home'?{'background-color':'#25261D'}:{'background-color':'#0A0E08'}]"
        @click="$parent.currentTab = 'timer'; selectedTab = 'home'"><img src="../../assets/home.png" alt=""></button>

        <button class="tab"
        :style="[selectedTab == 'history'?{'background-color':'#25261D'}:{'background-color':'#0A0E08'}]"
        @click="$parent.currentTab = 'history'; selectedTab = 'history'"><img src="../../assets/history.png" alt=""></button>

    </div>
</template>

<script>
export default {
    data () {
        return {
            selectedTab: 'home'
        }
    }
}

</script>

<style scoped>

    #root {
        position: absolute;
        z-index: 900;
        bottom: 0;
        width: 100vw;
        height: 64px;
        background-color: #0A0E08;
        text-align: center;
        display: flex;
        justify-content: center;
        z-index: 999;
    }

    button {
        height: 64px;
        width: 64px;
        margin: 0 12px;
        border: none;
        background-color: #0A0E08;
        transition: .15s;
    }

    button:hover {
        background-color: #0e140b;
        transition: .15s;
    }

    img {
        width: 32px;
    }

</style>