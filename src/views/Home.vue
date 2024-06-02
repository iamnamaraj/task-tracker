<template>
  <div class="home">
    <div v-if="tasks.length">
      <FilterTask @filterChange="current = $event"  :current="current" />
      <div v-for="task in filteredTask" :key="task.id">
        <SingleTask :task="task" @delete="handelDelete"  @complete="handelComplete" />
      </div>
    </div>
  </div>
</template>

<script>
  import SingleTask  from '../components/SingleTask.vue';
  import FilterTask from '../components/FilterTask.vue'

export default {
  name: 'Home',
  components: {
    SingleTask,FilterTask
  },

  data(){
    return {
      tasks: [],
      current:'all',
    }
  },
  methods:{
    handelDelete(id){
      this.tasks = this.tasks.filter((task) => {
        return task.id !== id
      })
    },
    handelComplete(id){
      let p = this.tasks.find(task => {
        return task.id === id
      });
      p.complete = !p.complete
    }
  },
  computed:{
    filteredTask(){
      if(this.current === 'completed'){
        return this.tasks.filter(task=> task.complete)
      }
      if(this.current === 'ongoing') {
        return this.tasks.filter(task=> !task.complete)
      }else{
        return this.tasks
      }
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
