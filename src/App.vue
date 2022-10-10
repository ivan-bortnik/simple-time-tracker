<template>
  <div id="app">

    <timer v-if="currentTab == 'timer'"
    :project="projects[currentTask.project].name"
    :task="projects[currentTask.project].tasks[currentTask.task].name"></timer>
    <projects-list v-if="currentTab == 'projects'" :projects="projects"></projects-list>

    <tab-bar></tab-bar>

  </div>
</template>

<script>
import TabBar from './components/TabBar/TabBar.vue';
import Timer from './components/Timer/Timer.vue';
import ProjectsList from './components/ProjectsList/ProjectsList.vue';

export default {
  components: {
    'tab-bar': TabBar,
    'timer': Timer,
    'projects-list': ProjectsList
  },
  data () {
    return {
      currentTab: 'timer',

      currentTask: {
        project: 0,
        task: 0
      },

      projects: [
        {
          name: "Lorem bite",
          client: "Dolor",
          colorTag: 1,
          tasks: [
            { name: "Sit amet consequitum", elapsedTime: 0 },
            { name: "Sucer des queues", elapsedTime: 0 }
          ]
        }
      ]
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Nunito:wght@200;300;500;600;700&display=swap');

#app {
  position: absolute;
  background-color: #36352A;
  width: 100vw;
  height: 100vh;
  font-family: 'Nunito';
  overflow: hidden;
}
</style>
