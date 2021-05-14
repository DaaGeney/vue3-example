<template >
    <FormInput />
</template>

<script>
import FormInput from './components/Challenge.vue'

export default {
    name: 'App',
    components: {
        FormInput
    },
    data: () => ({
        tasks: []
    }),
    methods: {
        createTask(task) {
            console.log(this.tasks);
            this.tasks.push(task);
            console.log(this.tasks);
        },
        completeTask(taskText) {
            for (let i = 0; i < this.tasks.length; i++) {
                let task = this.tasks[i];
                if (taskText === task.text) {
                    task.completed = !task.completed;
                }
            }
        }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
