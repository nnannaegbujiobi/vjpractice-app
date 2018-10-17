

<template>
  <div class="home">
    <div>
      <h5>total tasks: {{tasks.length}}</h5>
      <div>
    <button v-on:click="removeCompletedTasks()">Clear Completed Tasks</button>
  </div>
    </div>
    
    <li v-for="task in tasks">{{task.id}}: {{task.text}} : {{task.complete}}
    <h3 v-on:click="toggleComplete(task)">{{task.text}}</h3>
    <h4 v-bind:clase ="{strike: !task.text}"></h4>

    </li>

    <h2> Add Task:</h2>
  
    task: <input v-model="newTask.text">
    done: <input v-model="newTask.complete">
    id: <input v-model="newTask.id">
    
  <button v-on:click="addTask()">Add task</button>

<p> {{newTask}}</p>

  </div>
</template>

<style>
  .strike {
    text-decoration: line-through;
  }
</style>

<script>
  var axios = require("axios");
export default {
    data: function() {
      return { 
        tasks: [],
        newTask: {id:"",text:"",complete:true}
   
      };
    },
    created: function() {
      axios.get("http://localhost:3000/tasks").then(function(response) {
        console.log(response.data);
        this.tasks = response.data;
      }.bind(this));
    },
    methods: {
      addTask: function() {
        this.tasks.push(this.newTask);
        var params = {
          name: this.newTask.text,
          complete: this.newTask.complete 
        };
        axios.post("http://localhost:3000/api/tasks",params).then(function(response) {
          this.tasks.push(response.data);
          this.newTask.text = "";
          this.newTask.complete = "";
        }.bind(this));
      }


  





    // addTask: function() {
    //     if (this.newTask.text) {
    //       this.tasks.push(this.newTask);
    //       this.newTask.text = "",
    //       this.newTask = {id:"",text:"",complete:""};
    //     } else {
    //       this.error = "you must enter text!";
    //     }
    },
    toggleComplete: function(task) {
      task.complete = !task.complete;
    },

    numberOfIncompleteTasks: function() {
      var count = 0;
      for (var i = 0; i < this.tasks.length; i++) {
        if (!this.tasks[i].completed) {
          count += 1;
        }
      }
      return count;
  
    
    },
    computed: {}
  
};
</script>
