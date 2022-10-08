<template>
    <div id="root">

        <h1>Projects</h1>

        <div
        class="project"
        v-for="obj in projects"
        :key="obj.name"
        :style="{'border-color': getColor(obj.colorTag)}">
            <p class="project-name">{{ obj.name }}</p>
            <p class="project-client">{{ obj.client }}</p>
        </div>

        <p class="add-project" @click="isCreateProjectWindowVisible = true">+ ADD PROJECT</p>
        <create-project v-if="isCreateProjectWindowVisible"/>

    </div>
</template>

<script>
import CreateProject from '../CreateProject/CreateProject.vue';

export default {
    props: ["projects"],
    components: {
        'create-project': CreateProject
    },
    data () {
        return {
            isCreateProjectWindowVisible: false
        }
    },
    methods: {
        getColor (tagID) {
            return ["#b52616", "#46b516", "#1650b5", "#a10e97", "#e8c70c", "#ffffff"][tagID];
        }
    }
}
</script>

<style scoped src="./ProjectsList.css">
    
</style>