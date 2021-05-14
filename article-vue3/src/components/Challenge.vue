<template>
    <div class="task-list">
        <h1> Total Tasks: {{tasks.length}}</h1>
        <div class="task-section">
            <h4>Task Completed: {{completed}}  </h4>
            <h4>Task Incompleted: {{incompleted}} </h4>
        </div>
        <form  @submit.prevent="createTask">
            <label class="label" for="task">Nueva tarea:</label>
            <input class="input" type="text" v-model="newTask" id="task" />
            <button class="button" type="submit">Crear tarea</button>
        </form>
        <ul class="list">
        <li
            class="task"
            v-for="(task, i) in tasks"
            :key="'task' + i"
            :class="{completed: task.completed}"
            @click="completeTask(task.description)"
        >{{task.description}}</li>
        </ul>
    </div>
</template>

<script>
export default {
    name: "TodoList",
    data: () => ({
        newTask: "",
        tasks: [],
        completed: 0,
        incompleted: 0
    }),
    watch: {
        tasks: {
            handler: function (val) {
                const listCompleted = val.filter(e => e.completed)
                this.completed = listCompleted.length
                this.incompleted = val.length - listCompleted.length
            }, deep: true
        },
    },
    methods: {
        createTask() {
            let task = {
                description: this.newTask,
                completed: false
            };
            const alreadyExists = this.tasks.find(e => e.description === task.description);
            if (!alreadyExists && task.description !== '') {
                this.tasks.push(task)
                this.newTask = "";
            } else { 
                alert('Probably it already exists') 
            }
            console.log(this.tasks);
        },
        completeTask(taskDescription) {
            for (let i = 0; i < this.tasks.length; i++) {
                let task = this.tasks[i];
                if (taskDescription === task.description) {
                    task.completed = !task.completed;
                }
            }
        }
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