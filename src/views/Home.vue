<template>
  <div class="home">
    <FilterNav :current="current" @filterChange="current = $event" />  <!--when we hear a filterChange event then we update the current value by the
     argument which was passed while emitting the event($event)-->
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">   <!--each time we pass through a diffrent project we pass a different project as an prop to the component-->
        <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete" /> <!-- @delete that's the name of the event we are listening for-->
      </div>
    </div>
  </div>
</template>


<script>
import SingleProject from '../components/SingleProject.vue'
import FilterNav from '../components/FilterNav.vue'

export default {
  name: 'Home',
  components: { SingleProject, FilterNav },
  data() {
    return {
      projects: [],
      current: 'all',
    };
  },
  mounted() {
    fetch('http://localhost:3000/projects')
      .then(res => res.json())
      .then(data => this.projects = data)
      .catch(err => console.log(err))
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter(project => {
        return project.id !== id
      })
    },
    handleComplete(id) {
      let p = this.projects.find(project => {
        return project.id === id
      })
      p.complete = !p.complete 
    }
  },
  computed: {
    filteredProjects() {
      if (this.current === 'completed') {
        return this.projects.filter(project => project.complete)
      }
      if (this.current === 'ongoing') {
        return this.projects.filter(project => !project.complete)
      }
      return this.projects
    }
  },
}
</script>

