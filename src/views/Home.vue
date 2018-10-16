

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h1>{{secondMessage}}</h1>
    <li v-for="task in tasks">{{task.id}}: {{task.text}} : {{task.complete}}</li>

    <h2> Add Task:</h2>
  
    task: <input v-model="newTask.text">
    done: <input v-model="newTask.complete">
    id: <input v-model="newTask.id">
    
  <button v-on:click="addTask()">Add task</button>

<p> {{newTask}}</p>

  </div>
</template>

<style>
</style>

<script>
export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      secondMessage: "To do list",
      tasks: [
        {
          id:1,
          text: "Take out the garbage",
          complete: "not completed"


        },
        {
          id:2,
          text:"clean the house",
          complete:"completed"

        },
        {
          id:3,
          text:"pick up the kids",
          complete:"completed"
        }

      ],
      newTask: {id:"",text:"",complete:""}


    };
  },
  created: function() {},
  methods: {
    addTask: function() {
      if (this.newTask.text) {
        this.tasks.push(this.newTask);
        this.newTask.text = "",
        this.newTask = {id:"",text:"",complete:""};
      } else {
        this.error = "you must enter text!"
      }
    }
  },
  computed: {}
};

</script>
