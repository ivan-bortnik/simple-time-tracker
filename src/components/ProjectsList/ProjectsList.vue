<template>
    <div id="root">

        <h1>Projects</h1>

        <div class="project" v-for="obj in projects" :key="obj.name" :style="{'border-color': obj.colorTag}">
            <p class="project-name">{{ obj.name }}</p>
            <p class="project-client">{{ obj.client }}</p>
        </div>

        <p class="add-project">+ ADD PROJECT</p>
        <create-project/>

    </div>
</template>

<script>
import CreateProject from '../CreateProject/CreateProject.vue';

export default {
    props: ["projects"],
    components: {
        'create-project': CreateProject
    }
}
</script>

<style scoped src="./ProjectsList.css">
    
</style>