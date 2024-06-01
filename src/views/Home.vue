<template>
  <div class="home">
    <div v-if="tasks.length">
      <div v-for="task in tasks" :key="task.id">
        <SingleTask :task="task" @delete="handelDelete" />
      </div>
    </div>
  </div>
</template>

<script>
  import SingleTask  from '../components/SingleTask.vue';

export default {
  name: 'Home',
  components: {
    SingleTask,
  },

  data(){
    return {
      tasks: []
    }
  },
  methods:{
    handelDelete(id){
      this.tasks = this.tasks.filter((task) => {
        return task.id !== id
      })
    }
  },
  mounted(){
    fetch('http://localhost:3000/tasks')
    .then(res => res.json())
    .then(data => this.tasks = data)
    .catch(err => console.log(err.message))
  }

}
</script>
