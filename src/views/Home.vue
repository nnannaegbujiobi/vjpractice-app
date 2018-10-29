run

<template>
  <div class="home">
    <div>
      <h5>total tasks: {{tasks.length}}</h5>
      <div>

  </div>
    </div
    <div class="row">
        <div class="col-md-4">
          <div class="form-group">
            <!-- <input v-model="taskFilter" list="text" class="form-control" placeholder="Search tasks" type="text"> -->
          </div>
        </div>
    <div>
      <li v-for="error in errors">{{error}}</li>
    </div>
    
    <!-- < --><!-- li v-for="task in tasks">{{task.id}}: {{task.text}} : {{task.complete}}
    <h3 v-on:click="toggleComplete(task)">{{task.text}}</h3>
    <h4 v-bind:clase ="{strike: !task.text}"></h4>


    </li> -->

    <h2> Add Task:</h2>
  
    task: <input v-model="newTask.text">
    done: <input v-model="newTask.complete">
    id: <input v-model="newTask.id">
    
  <button v-on:click="addTask()">Add task</button>

<p> {{newTask}}</p>

    <div v-for="task in orderBy(filterBy(tasks, taskFilter, 'text'), sortAttribute, sortAscending)" class="col-md-4 text-center item-block" v-bind:key="task.id">
            <h3 v-on:click="toggleBioVisible(task)">{{ task.text}}</h3>
            <p v-bind:class="{strike: !task.bioVisible}">{{ task.bio }}</p>
            <!-- <p><a v-on:click="deleteTask(task)" class="btn btn-primary btn-outline with-arrow">Delete <i class="icon-arrow-right"></i></a></p> -->
      </div>
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
        newTask: {id:"",text:"",complete:""},
        errors: [],
        taskFilter: ""
   
      };
    },
    created: function() {
      axios.get("http://localhost:3000/api/tasks").then(function(response) {
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
          
        }).catch(error => {
          this.errors = error.response.data.errors;
        });
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
    toggleBioVisible: function(task) {
      task.bioVisible = !task.bioVisible;
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
