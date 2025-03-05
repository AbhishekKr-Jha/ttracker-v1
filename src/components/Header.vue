<script>
import Button from './Button.vue';

export default {
  name: "HeaderComponent", 
  props: {
    showForm: Boolean
  },
  components:{
    Button
  }
};
</script>



<template>

<div class="">
    <h1>T-Tracker</h1>
    <br/>
<Button :showForm="showForm" @toggle-add-task="$emit('toggle-add-task')" />
</div>

</template>



<style >



</style>