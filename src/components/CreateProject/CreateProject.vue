<template>
    <div id="root">

        <div class="container">

            <h2>Add Project</h2>

            <form action="">
                <div class="project-form-element">
                    <label for="project-name">Project Name</label><br>
                    <input type="text" name="project-name" id="project-name" v-model="projectName">
                </div>

                <div class="project-form-element">
                    <label for="client-name">Client</label><br>
                    <input type="text" name="client-name" id="client-name" v-model="projectClient">
                </div>
                
                <div class="color-tag-selection">
                    <label>Tag</label><br/>
                    <input type="radio" name="color-tag" id="color-1" style="background-color: #b52616" v-model="colorTag" value="0">
                    <input type="radio" name="color-tag" id="color-2" style="background-color: #46b516" v-model="colorTag" value="1">
                    <input type="radio" name="color-tag" id="color-3" style="background-color: #1650b5" v-model="colorTag" value="2">
                    <input type="radio" name="color-tag" id="color-4" style="background-color: #a10e97" v-model="colorTag" value="3">
                    <input type="radio" name="color-tag" id="color-5" style="background-color: #e8c70c" v-model="colorTag" value="4">
                    <input type="radio" name="color-tag" id="color-5" style="background-color: #ffffff" v-model="colorTag" value="5">
                </div>

            </form>
            
            <button @click="createProject" id="create">+ CREATE</button>
            <button @click="cancel" id="cancel">CANCEL</button>
        </div>

    </div>
</template>

<script>
export default {
    data () {
        return {
            projectName: '',
            projectClient: '',
            colorTag: ''
        }
    },
    methods: {
        createProject () {
            // Get data
            let name = this.projectName;
            let client = this.projectClient;
            let tag = parseInt(this.colorTag);

            // TODO: Validate data
            
            // Assign ID
            let id = 0;
            if (this.$parent.projects.length > 0) {
                let id = this.$parent.projects.at(-1).id + 1;
            }
            // TODO: Check compatibility of at() method

            // Send data
            this.$parent.projects.push({
                id,
                name: name,
                client: client,
                colorTag: tag,
                tasks: [{ id: 0, name: "First task", elapsedTime: 0 }]
            });
            this.$parent.$parent.save();
            this.$parent.isCreateProjectWindowVisible = false;
        },

        cancel () {
            this.$parent.isCreateProjectWindowVisible = false;
        }
    }
}
</script>

<style scoped src="./CreateProject.css"></style>