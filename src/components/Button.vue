
<script>
export default{
    name:'Button',
    props: {
        showForm: Boolean
    },
    methods:{
        toggleView(){
            console.log("something is shoen")
this.$emit('toggle-add-task')
        }
    }
}

</script>

<template>
    <button @click="toggleView()" type="button" >  {{ showForm ? 'View Task List' : 'Add Task' }}</button>
</template>