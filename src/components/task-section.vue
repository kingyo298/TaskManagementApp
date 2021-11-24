<template>
  <div class="mx-2 col-2 px-0">
    <div class="p-4 box">
      <input
        type="text"
        @change="addSectionTitle($event.target.value)">
      <app-task
        v-for="(task,index) in sections[sectionId].tasks"
        :key="index"
        :taskId="index"
        :sections="sections"
        :sectionId="sectionId"
        :task="task"
        @edit="editable"
        @favorite="favorite"
        @check="check"
        @deleteTask="deleteTask($event)"
        @transferSection="transferSection"></app-task>
      <div>
        <button @click="addTask"><i class="fas fa-plus"></i></button>
      </div>
    </div>
  </div>
</template>
<script>
import Task from './task.vue';
import NewTask from './task-new.vue';
let todoId = 0;
export default {
  props: ["sectionId","sections"],
  components:{
    appTask : Task,
    appNewTask: NewTask,
  },
  methods: {
    addTask : function(){
      this.sections[this.sectionId].tasks.push({
        id: todoId++,
        text: "",
        favoriteTask: false,
        checkedTask: false,
        isEditable: false
      });
    },
    favorite : function(taskObj){
      taskObj.favoriteTask = !taskObj.favoriteTask;
    },
    check : function(taskObj){
      taskObj.checkedTask = !taskObj.checkedTask;
    },
    editable : function(taskObj){
      taskObj.isEditable = !taskObj.isEditable;
    },
    deleteTask : function(taskObj){
      this.sections[this.sectionId].tasks = this.sections[this.sectionId].tasks.filter(task => task.id !== taskObj.id);
    },
    addSectionTitle : function(title){
      this.sections[this.sectionId].sectionTitle = title;
    },
    transferSection : function(...args){
      const [location,task] = args;
      let temp = task;
      this.deleteTask(task);
      this.sections[location].tasks.push(temp);
    }
  }
}
</script>
<style>
input,textarea{
  box-shadow: inset 2px 2px 5px #BABECC, inset -5px -5px 10px #FFF;
  width: 100%;
  box-sizing: border-box;
  transition: all 0.2s ease-in-out;
  appearance: none;
  padding: 0.5rem;
}
input:focus,textarea:focus{
  box-shadow: inset 1px 1px 2px #BABECC, inset -1px -1px 2px #FFF;
}
.box{
  border-radius: 4px;
  background-color: #E0E5EC;
  box-shadow: 9px 9px 16px rgb(163,177,198,0.6), -9px -9px 16px rgba(255,255,255, 0.5);
}
.box__inner{
  border-radius: 4px;
  background-color: #E0E5EC;
  box-shadow: 2.25px 2.25px 4px rgb(163,177,198,0.6), -2.25px -2.25px 4px rgba(255,255,255, 0.5);
}
</style>
