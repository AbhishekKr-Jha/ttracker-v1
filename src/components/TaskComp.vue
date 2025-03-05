
<script>
import Task from './Task.vue';

export default{
    name:'TaskComp',
    props:{
        taskList:Array
    },
    components:{
Task
    },
    computed: {
    isTaskListEmpty() {
      return this.taskList.length === 0;
    }
}
}


// console.log(this.taskList)


</script>


<template>
    <div class="listContainer">
    <div v-show="!isTaskListEmpty"  v-for="item in taskList" :key="item.id">
    <Task @edit-task="$emit('edit-task',item.id)" @delete-task="$emit('delete-task',item.id)" :task="item" />
</div>
<h1 style="" v-show="isTaskListEmpty">No Task Yet!🎈 Add Some.</h1> 
</div>


</template>



<style scoped>

.listContainer{
    width: 97%;
    display: flex;
    gap:20px; 
    flex-wrap: wrap;
    align-items: center; justify-content: center;
   margin:20px 10px;
   
}




</style>