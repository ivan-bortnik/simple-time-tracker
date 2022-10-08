<template>
<div id="root">

    <div class="popup">
        <h2>rly?</h2>
        <button style="background-color: #34870B" @click="confirm">YES</button>
        <button style="background-color: #CF2E2E" @click="cancel">CANCEL</button>
    </div>

</div>    
</template>

<script>

export default {

    methods: {
        confirm () {
            this.$parent.$data.needConfirmation = false;
            this.$parent.resetTimer();
        },

        cancel () {
            this.$parent.$data.needConfirmation = false;
            this.$parent.start();
        }
    }

}

</script>

<style scoped>

    #root {
        position: absolute;
        height: 100vh;
        width: 100vw;
        background-color: rgba(0, 0, 0, .8);
        z-index: 999;
    }

    .popup {
        position: absolute;
        top: 50vh;
        width: 100vw;
        transform: translateY(-50%);
        background-color: #25261D;
        /* height: 42vh; */    
    }

    h2 {
        margin: 32px 0;
    }

    button {
        margin: 16px;
        border: none;
        border-radius: 4px;
        padding: 8px;
        width: 64px;
        color: white;
        transition: .15s;
    }

    button:hover {
        transform: scale(1.1);
        transition: .15s;
    }

    button:active {
        transform: scale(.7);
        transition: .15s;
    }

</style>