<template>
  <div id="app">

    <p id="no-project" v-if="projects.length == 0">You don't have any project to work on</p>
    
    <timer v-if="currentTab == 'timer' && projects.length > 0"
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

      projects: []
    }
  },

  created () {
    this.load();
  },

  methods: {
    load () {
      if (localStorage.getItem('project') !== null) {
        let dataAsString = localStorage.getItem('projects');
        this.projects = JSON.parse(dataAsString);
      }
    },

    save () {
      let dataAsString =  JSON.stringify(this.projects);
      localStorage.setItem('projects', dataAsString);
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

#no-project {
  position: absolute;
  width: 100vw;
  color: #999;
  font-size: 24pt;
  font-weight: bolder;
  text-align: center;
  margin: 30vh 0;
}
</style>
