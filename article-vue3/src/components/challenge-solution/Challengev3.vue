<template>
    <div class="task-list">
        <h1> Total Tasks: {{data.tasks.length}}</h1>
        <div class="task-section">
            <h4>Task Completed: {{data.completed}}  </h4>
            <h4>Task Incompleted: {{data.incompleted}} </h4>
        </div>
        <form  @submit.prevent="createTask">
            <label class="label" for="task">Nueva tarea:</label>
            <input class="input" type="text" v-model="data.newTask" id="task" />
            <button class="button" type="submit">Crear tarea</button>
        </form>
        <ul class="list">
        <li
            class="task"
            v-for="(task, i) in data.tasks"
            :key="'task' + i"
            :class="{completed: task.completed}"
            @click="completeTask(task.description)"
        >{{task.description}}</li>
        </ul>
    </div>
</template>

<script>
import { reactive, watch } from 'vue';

export default {
    name: "TodoList",
    setup() {
        const data = reactive({
            newTask: '',
            tasks: [],
            completed: 0,
            incompleted: 0
        });

        watch(() => data.tasks, (current) => {
            const listCompleted = current.filter(e => e.completed)
            data.completed = listCompleted.length
            data.incompleted = current.length - listCompleted.length
        }, { deep: true });

        const createTask = () => {
            let task = {
                description: data.newTask,
                completed: false
            };

            const alreadyExists = data.tasks.find(e => e.description === task.description);

            if (!alreadyExists && task.description !== '') {
                data.tasks.push(task)
                data.newTask = "";
            } else if (task.description === '') { 
                alert('Not empty tasks') 
            } else {
                alert('Probably it already exists') 
            }

            console.log(data.tasks);
        }

        const completeTask = (taskDescription) => {
            for (let i = 0; i < data.tasks.length; i++) {
                let task = data.tasks[i];
                if (taskDescription === task.description) {
                    task.completed = !task.completed;
                }
            }
        }

        return { createTask, completeTask, data }
        
    }
};
</script>

<style scoped>
.task-list {
  width: 800px;
  max-width: 100%;
  height: 80vh;
  margin: 0px auto;
  background: white;
  border-radius: 12px;
  padding: 30px;
  box-shadow: 0px 10px 22px -1px rgba(0,0,0,0.25);
  margin-top: 10px;
}
.form {
  background: white;
  border-radius: 12px;
  padding: 30px;
  box-shadow: 0px 10px 22px -1px rgba(0,0,0,0.25);
  margin-top: 10px;
}
.label {
  display: block;
  margin-bottom: 10px;
}
.input {
  height: 35px;
  width: 80%
}
.button {
  margin-left: 20px;
  height: 35px;
  border: none;
  border-radius: 5px;
  box-shadow: 0 1px 4px rgba(0, 0, 0, .2);
  background-color: #f05d22;
  color: #ecf0f1;
  cursor: pointer
}
.list {
  margin-top: 40px;
}
.task {
  cursor: pointer;
  margin: 10px 0;
  list-style-type: circle;
}
.task-section {
    display: flex;
    justify-content: space-around;
}
.completed {
  text-decoration: line-through;
  color: lightgrey;
}
</style>