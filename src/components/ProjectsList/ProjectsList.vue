<template>
    <div id="root">

        <h1>Projects</h1>


        <div class="container">
            <div
            class="project"
            v-for="(obj, projectID) in projects"
            :key="projectID"
            :style="{'border-color': getColor(obj.colorTag)}">
                <p class="total-time">{{ formatTime(getTotalTime(projectID)) }}</p>

                <p class="project-name">{{ obj.name }}</p>
                <p class="project-client">{{ obj.client }}</p>
    
                <ul class="tasks">
                    <li v-for="(task, taskID) in obj.tasks" :key="taskID">
                        <span class="elapsed-time" @click="setTask(projectID, taskID)">{{ formatTime(task.elapsedTime) }}</span>
                        <input type="text" v-model="task.name" placeholder="Task name">
                    </li>
    
                    <li class="add-task" @click="addTask(projectID)">
                        + Add Task
                    </li>
                </ul>
            </div>
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
            isCreateProjectWindowVisible: false,
        }
    },
    methods: {
        getColor (tagID) {
            // Simply returns the hex value from the premade pallete
            // Colors are RED; GREEN; BLUE; PURPLE; YELLOW; WHITE
            return ["#b52616", "#46b516", "#1650b5", "#a10e97", "#e8c70c", "#ffffff"][tagID];
        },

        formatTime (time) {
            // Return elapsed time in a string in a HH:MM:SS format
            let hrs = `${Math.floor(time / 3600)}`.padStart(2, '0');
            let min = `${Math.floor(time % 3600 / 60)}`.padStart(2, '0');
            let sec = `${time % 60}`.padStart(2, '0');

            return `${hrs}:${min}:${sec}`;
        },
        
        addTask (idx) {
            // Assign ID
            let id = this.projects[idx].tasks.at(-1).id + 1;
            console.log(id);
            this.projects[idx].tasks.push({id: id, name: "Task", elapsedTime: 0});
        },

        setTask (projectIdx, taskIdx) {
            this.$parent.currentTask = { project: projectIdx, task: taskIdx };
            this.$parent.currentTab = 'timer';
        },

        getTotalTime (projectIdx) {
            let totalTime = 0;

            for (let i = 0; i < this.projects[projectIdx].tasks.length; i++) {
                totalTime += this.projects[projectIdx].tasks[i].elapsedTime;
            }

            return totalTime;
        }
    }
}
</script>

<style scoped src="./ProjectsList.css">
    
</style>