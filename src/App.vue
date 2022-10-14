<template>
  <div id="app">

    <p id="no-project" v-if="projects.length == 0">You don't have any project to work on</p>
    
    <timer v-if="currentTab == 'timer' && projects.length > 0"
    :workingon="`${projects[currentTask.project].name} - ${projects[currentTask.project].tasks[currentTask.task].name}`"></timer>
    <projects-list v-if="currentTab == 'projects'" :projects="projects"></projects-list>
    <history v-if="currentTab == 'history'"></history>

    <tab-bar v-if="!isTimerRunning"></tab-bar>

  </div>
</template>

<script>
import TabBar from './components/TabBar/TabBar.vue';
import Timer from './components/Timer/Timer.vue';
import ProjectsList from './components/ProjectsList/ProjectsList.vue';
import History from './components/History/History.vue';


import { ipcRenderer } from 'electron';

export default {
  components: {
    'tab-bar': TabBar,
    'timer': Timer,
    'projects-list': ProjectsList,
    'history': History
  },
  data () {
    return {
      currentTab: 'timer',
      isTimerRunning: false,
      
      // Currently, those refers to the index of the task or project in
      // the projects array, in the future, they should refer to their 
      // ID instead
      currentTask: {
        project: 0,
        task: 0
      },

      projects: [],

      history: []
    }
  },

  mounted () {
    //console.log(fs);
    this.load();
  },


  methods: {
    load() {       
      ipcRenderer.invoke('load-user-data').then((result) => {
        let userData = JSON.parse(result);
        console.log(userData);
        this.projects = userData.projects;
        this.history = userData.history;
      })
    },

    async save() {
      const data = JSON.stringify({
        projects: this.projects,
        history: this.history
      }); // load it from your source            
      ipcRenderer.invoke('save-user-data', { data });
    },

    saveToHistory (elapsedTime) {
      const today = new Date();
      const yyyy = today.getFullYear();
      let mm = today.getMonth() + 1; // Months start at 0!
      let dd = today.getDate();

      if (dd < 10) dd = '0' + dd;
      if (mm < 10) mm = '0' + mm;

      const formattedDate = dd + '/' + mm + '/' + yyyy;
      
      this.history.unshift({
        projectID:  this.projects[this.currentTask.project].id,
        taskID: this.projects[this.currentTask.project].tasks[this.currentTask.task].id,
        date: formattedDate,
        elapsedTime: elapsedTime,
        colorTag: this.projects[this.currentTask.project].colorTag,
        name: `${this.projects[this.currentTask.project].name} - ${this.projects[this.currentTask.project].tasks[this.currentTask.task].name}`
      })
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
  z-index: 1;
}
</style>
