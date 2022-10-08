<template>
    <div id="root">

        <div class="container">

            <h2>Add Project</h2>

            <form action="">
                <div class="project-form-element">
                    <label for="project-name">Project Name</label><br>
                    <input type="text" name="project-name" id="project-name">
                </div>

                <div class="project-form-element">
                    <label for="client-name">Client</label><br>
                    <input type="text" name="client-name" id="client-name">
                </div>
                
                <div class="color-tag-selection">
                    <p>Tag  </p>
                    <input type="radio" name="color-tag" id="color-2">
                    <input type="radio" name="color-tag" id="color-1">
                    <input type="radio" name="color-tag" id="color-3">
                    <input type="radio" name="color-tag" id="color-4">
                    <input type="radio" name="color-tag" id="color-5">
                </div>
            </form>

        </div>

    </div>
</template>

<script>
export default {
    
}
</script>

<style scoped>

#root {
    color: white;
    position: absolute;
    top: 0;
    background-color: rgba(0, 0, 0, .8);
    height: 100vh;
    width: 100vw;
    z-index: 99999;
}

.container {
    position: absolute;
    background-color: #36352A;
    width: 90vw;
    height: 80vh;
    position: absolute;
    left: 50%;
    top: 50%;
    -webkit-transform: translate(-50%, -50%);
    transform: translate(-50%, -50%);
}

h2 {
    margin: 0;
    padding: 16px;
}

.project-form-element {
    margin: 16px 8px;
}

.color-tag-selection {
    margin: 16px 8px;
}

.color-tag-selection p {
    margin: 0;
}

.color-tag-selection input {
    float: left;
    margin: 6px;
}

</style>