<template>
  <div class="task-list">
    <h1>{{tasks.length}} Tasks</h1>
    <form class="form" @submit.prevent="createTask">
      <label class="label" for="task">Nueva tarea:</label>
      <input class="input" type="text" v-model="newTask" id="task" />
      <input class="button" type="submit" value="Crear tarea" />
    </form>
    <ul class="list">
      <li
        class="task"
        v-for="(task, i) in tasks"
        :key="'task' + i"
        :class="{completed: task.completed}"
        @click="completeTask(task.text)"
      >{{task.text}} - <button  @click="deleteTask(task.text, task.completed)"><img src="../assets/basura.png" height="20"/></button></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "TodoList",
  data: () => ({
    newTask: "",
    tasks: [{text: 'Una prueba 1', completed: false},
            {text: 'Una prueba 2', completed: false},
            {text: 'Una prueba 3', completed: false},
            {text: 'Una prueba 4', completed: false},
            {text: 'Una prueba 5', completed: false},
            {text: 'Una prueba 6', completed: false}
            ]
  }),
  methods: {
    createTask() {
      let task = {
        text: this.newTask,
        completed: false
      };
      this.tasks.push(task);
      this.newTask = "";
      console.log(this.tasks);
    },
    completeTask(taskText) {
      for (let i = 0; i < this.tasks.length; i++) {
        let task = this.tasks[i];
        if (taskText === task.text) {
          task.completed = !task.completed;
        }
      }
    },
    deleteTask (taskText, completed){
      for (let i = 0; i < this.tasks.length; i++) {
        let task = this.tasks[i];
        if (taskText === task.text) {
         
          this.tasks.splice(i,1); 
          
          console.log(i);
          console.log(completed);
          console.log(this.tasks);
          console.log(this.tasks.length);
          let nuevoArray = this.tasks[i];
          
            nuevoArray.completed = true;
          
          
          console.log(nuevoArray);
        }
   
      }
      console.log(completed);
      
    }

  }
};
</script>

<style scoped>
.task-list {
  width: 800px;
  max-width: 100%;
  margin: 0px auto;
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
  border-radius: 5px;
}
.button {
  margin-left: 20px;
  height: 35px;
  border: none;
  border-radius: 5px;
  box-shadow: 0 1px 4px rgba(0, 0, 0, .2);
  background-color: #2ecc71;
  color: #ecf0f1;
  cursor: pointer
}
.list {
  margin-top: 40px;
  margin-right: 200px;
  text-align: left;
}

.task {
   cursor: pointer;
}

.completed {
  text-decoration: line-through;
  color: lightgrey;
}
</style>