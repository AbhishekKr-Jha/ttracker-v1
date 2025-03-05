
<script>
import { onMounted } from 'vue'

export default{
    name:'AddTask',
    props: {
    updation:Boolean,
    dataToUpdate:Object
    },
    data(){
        return{
            // id:'89',
            task:!this.updation?'':this.dataToUpdate?.task,
            day:!this.updation?'':this.dataToUpdate?.day,
            reminder:!this.updation?false:this.dataToUpdate?.reminder, 
        }
    },
    methods:{
        onSubmit(e){
            e.preventDefault()
            if(!this.task || !this.day){
                alert("plese fill all details")
                return
            }
            const newTask={
                id:!this.updation?String(Math.floor(Math.random()*100000)):this.dataToUpdate?.id, // on the basis of task addition or updation
                task:this.task,
                day:this.day,
            reminder:this.reminder ,
            
            }
            this.task=''
             this.day=''
             this.reminder = false
            // console.log("thr new tak is",newTask)
            this.$emit('add-task',newTask)   //same for add and update
        },
        
    }
    
}

</script>

<template>
 <form @submit="onSubmit" style="margin: 30px 0;">

    <input class="formInput" v-model="task" type="text" placeholder="Enter Task Details" />
    <input class="formInput" v-model="day" type="text" placeholder="Enter the day ( Ex. Sunday )" />

    <label style="cursor: pointer;"><input type="checkbox"  v-model="reminder" >&nbsp;Do you need a reminder?</label>

    <button type="submit" >{{ updation?"Update":"Add" }}</button>

 </form>


</template>


<style scoped>
.formInput{
    width:350px;
    padding: 10px;
    border-radius: 10px;
}
form{
    display: flex;
    flex-direction: column;
    gap: 20px;
    justify-content: center;
    align-items: center;
}

@media screen and (max-width: 400px) {
.formInput{
    width: 96vw;
}
}


</style>