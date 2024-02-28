<script>
import ParamCont from './components/ParamCont.vue';
import TaskList from './components/TaskList.vue';

  export default{
    components: { ParamCont, TaskList },
    data(){
      return{
        taskArray:[
          
        ]
      }
    },
    methods:{
      addTask(task){
        this.taskArray.push(task)
        console.log(this.taskArray)
      }
    }
}
</script>

<template>
  <div class="appContainer">
    <ParamCont @newTaskCreated="addTask"></ParamCont>
    <TaskList :task-array="this.taskArray"></TaskList>
  </div>
</template>

<style>
  @font-face {
    font-family: 'Inter';
    src: url('./assets/fonts/Inter-VariableFont_slnt\,wght.ttf') format('truetype');
  }

  .appContainer{
    background-color: #1ABC9C;
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100%;
    font-family: 'Inter';
  }
</style>