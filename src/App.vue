<template>
  <div id="app">

    <timer v-if="currentTab == 'timer'"></timer>
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

      projects: [
                {
                    name: 'Hotel de la bite',
                    client: 'Borrione S.A.R.L',
                    colorTag: "#F00",
                    tasks: [
                        {name: 'Manger ta mere', time: 8754},
                        {name: 'Sucer ton pere', time: 69420}
                    ]
                },

                {
                    name: 'Hotel du cul',
                    client: 'Borrione S.A.R.L',
                    colorTag: "#00F",
                    tasks: [
                        {name: 'Manger ta mere', time: 8754},
                        {name: 'Sucer ton pere', time: 69420}
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
}
</style>
