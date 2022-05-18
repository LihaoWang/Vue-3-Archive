<template>
  <div class="home">
    <FilterNav @update-filter="current = $event" :current="current" />
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject
          :project="project"
          @delete-project="deleteProject"
          @toggle-complete="toggleComplete"
        />
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
      allProjects: [],
      projects: [],
      current: 'all',
    }
  },
  methods: {
    deleteProject(id) {
      console.log('delete')
      this.projects = this.projects.filter((project) => project.id !== id)
    },
    toggleComplete(id) {
      console.log('toggle complete')
      this.projects = this.projects.map((project) => {
        if (project.id === id) {
          project.complete = !project.complete
        }
        return project
      })
    },
    updateFilter(filter) {
      console.log('update filter')
      if (filter === 'all') {
        this.projects = this.allProjects
      } else if (filter === 'completed') {
        this.projects = this.allProjects.filter((project) => project.complete)
      } else if (filter === 'ongoing') {
        this.projects = this.allProjects.filter((project) => !project.complete)
      }
    },
  },
  mounted() {
    fetch('http://localhost:3000/projects')
      .then((res) => res.json())
      .then((data) => {
        this.projects = data
        this.allProjects = data
      })
      .catch((err) => console.log(err))
  },
  computed: {
    filteredProjects() {
      if (this.current === 'all') {
        return this.projects
      } else if (this.current === 'completed') {
        return this.projects.filter((project) => project.complete)
      } else if (this.current === 'ongoing') {
        return this.projects.filter((project) => !project.complete)
      }
    },
  },
}
</script>
