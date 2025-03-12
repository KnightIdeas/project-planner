<template>
  <div class="home">
    <FilterNav @filterChange="current = $event" :current="current"/>
    <div v-if="projects.length && current === 'all'">
      <div v-for="project in projects" :key="project.id">
    <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete"/>
  </div>
    </div>
    <div v-if="projects.length && current === 'completed'">
      <div v-for="project in projects" :key="project.id">
    <SingleProject v-if="project.complete" :project="project" @delete="handleDelete" @complete="handleComplete"/>
  </div>
    </div>
    <div v-if="projects.length && current === 'ongoing'">
      <div v-for="project in projects" :key="project.id">
    <SingleProject v-if="!project.complete" :project="project" @delete="handleDelete" @complete="handleComplete"/>
  </div>
    </div>
  </div>
</template>

<script>
import SingleProject from '@/components/SingleProject.vue';
import FilterNav from '@/components/FilterNav.vue';

export default {
  name: 'HomeView',
  components: {
    SingleProject,
    FilterNav
  },
  data() {
    return {
      projects: [],
      current: 'all'
    }
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((project) => {
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
  mounted() {
  fetch(`https://api.jsonbin.io/v3/b/${process.env.VUE_APP_JSONBIN_ID}`, {
    headers: {
      'X-Master-Key': process.env.VUE_APP_JSONBIN_MASTER_KEY, // Use env variable
      'X-Access-Key': process.env.VUE_APP_JSONBIN_ACCESS_KEY
    }
  })
  .then(res => res.json())
  .then(data => this.projects = data.record.projects) // Access 'record' key
  .catch(err => console.log(err.message));
}
}
</script>
