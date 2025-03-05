<script >
import Header from './components/Header.vue';
import TaskComp from './components/TaskComp.vue';
import AddTask from './components/AddTask.vue';


export default{
    name:'App',
    components:{
        Header,
        TaskComp,
        AddTask
    },
    data(){
        return{
            tasks:[],
            viewAddTaskForm:false,//toggling the view of form
            isUpdation:false,// checking that form is for adding new task or updating old task
            updationData:null //stores data that nees to be updated
        }
    },
    methods:{
// ---toggle the form-----
        toggleAddTask(){
            console.log("the task list data is",this.viewAddTaskForm)
        console.log("ok this is running")
        this.viewAddTaskForm=!this.viewAddTaskForm
        this.updationData=null
        this.isUpdation=false
    },


        // -----adding new task  with updation as well
        async addTask(task) {
//   console.log("task is", task);
 if(!this.isUpdation){
    const res = await fetch('http://localhost:5000/tasks', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(task),
  });

  const newTask = await res.json();
  this.tasks = [...this.tasks, newTask];
  this.viewAddTaskForm=false
  
 }
else{
    // console.log("the upadted data is",task.id)
 this.updatedTaskData(task.id,task)  
}
},



// -----fetching task data
async fetchTaskData(id) {
  const url = id ? `http://localhost:5000/tasks/${id}` : 'http://localhost:5000/tasks';
  const res = await fetch(url);
  const data = await res.json();

  return data;
},


// -------deleting task data
async deleteTask(id) {
    // console.log(id)
  const url = `http://localhost:5000/tasks/${String(id)}`;
  const res = await fetch(url, {
    method: 'DELETE',
  });

  if (res.status!==200) {
  alert("Someting went wrong in deletion!")
  }
  else{
    // alert("success")
  }

//   console.log("the response is",res.json())

  const updatedTasks = await this.fetchTaskData();
  this.tasks = updatedTasks;
},



// ---------updated tasks
async updatedTaskData(id, updatedData) {
    // console.log("---",typeof id)
    console.log("the passed updted data is",updatedData)
  const url = `http://localhost:5000/tasks/${String(id)}`;

  const res = await fetch(url, {
    method: "PUT", 
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(updatedData),
  });

  if (!res.ok) {
   alert("Failed to update task");
   return
  } 



  const updatedTasks = await this.fetchTaskData();
  this.tasks = updatedTasks;
  this.isUpdation=false
  this.updationData=null
  this.viewAddTaskForm=false

},


// ----getting task data using id for updation
async updateTask(id){
   const data= await this.fetchTaskData(id) 
   this.updationData=data
   this.viewAddTaskForm=true
   this.isUpdation=true
}
    },

    // on mounted running the get api function
  async  created(){
        this.tasks =await this.fetchTaskData()
    }
   
}


</script>

<template>

<div style="padding: 12px;" class="">

    <Header :showForm="viewAddTaskForm"  @toggle-add-task="toggleAddTask"  />
    <!-- --task for--- -->
  <div v-if="viewAddTaskForm" class="">
    <AddTask :dataToUpdate="updationData" :updation="isUpdation"  @add-task="addTask" />
  </div>
  <!-- ----------container of tasks---------- -->
<div v-if="!viewAddTaskForm" class="">
    <TaskComp @edit-task="updateTask" @delete-task="deleteTask" :taskList="tasks" />
</div>

</div>
</template>


<style >

*{margin: 0;padding: 0;box-sizing: border-box;}
button{
    padding:8px 20px;
    border-radius: 8px;
    cursor: pointer;
}
</style>