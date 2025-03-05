<script>
export default{
name:'Task',
props:{
    task:Object
},methods:{
    deleteTask(id){
        this.$emit('delete-task',id)
    },
    editData(id){
        this.$emit('edit-task',id)
    }
}

}
</script>


<template>

<div class="task-container">
    <div title="Reminder Indicator" v-show="task.reminder" class="reminderIndicator"></div>
    <h5 :class="{ 'reminder': task.reminder }">{{ task.task }}</h5>
    <p style="margin-top: 5px;">{{ task.day }}</p>

    <i @click="deleteTask(task.id)" style="position: absolute;top: 8px;right: 8px;cursor: pointer;" class="fa-solid fa-xmark "></i>
 <i @click="editData(task.id)" style="position: absolute;bottom: 8px;left: 8px;cursor: pointer;font-size: 15px;" class="fa-solid fa-pen"></i> 

</div>
</template>


<style scoped>
.reminder{
   color: green;
   /* font-size: 20px; */
  font-weight: 700;
}

p{
    font-size: 15px;
}

.task-container{
border: 2px solid black;
 
 width: 250px;
  text-align: center;
  position: relative;
  font-size: 20px;
  border-radius: 5px;
  padding: 10px 20px;

}

 @media screen and (max-width: 260px) {
  .task-container {
   font-size: 15px;
   width:94vw ;
  }

  p{
    font-size: 12px;
  }

} 


</style>