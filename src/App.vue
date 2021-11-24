<template>
  <div id="app">
    <div class="">
      <div class="mt-4 d-flex">
        <app-task-section
          v-for="(section,index) in sections"
          :key="index"
          :sectionId="index"
          :sections="sections"></app-task-section>
        <div class="px-2">
          <button class="p-3" @click="addSection">Add Section</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import TaskSection from './components/task-section.vue';
export default {
  data(){
    return {
      sections: [],
    }
  },
  components : {
    appTaskSection : TaskSection
  },
  methods : {
    addSection : function(){
      this.sections.push({
        sectionTitle: "",
        tasks:[{
          id: 0,
          text: "",
          favoriteTask: false,
          checkedTask: false,
          isEditable: false
        }]
      });
    },
  }
}
</script>
<style>
body{
  background-color: #EBECF0;
}
button,input,textarea{
  border: 0;
  outline: none;
  font-size: 1.0rem;
  background-color: #EBECF0;
  text-shadow: 1px 1px 0 #FFF;
}
textarea{
  resize: none;
}
button,input{
  border-radius: 2.0rem;
}
button{
  color: #61677C;
  font-weight: bold;
  box-shadow: -5px -5px 20px #FFF, 5px 5px 20px #BABECC;
  transition: all 0.2s ease-in-out;
  cursor: pointer;
  font-weight: 600;
}
button:hover{
  box-shadow: -2px -2px 5px #FFF, 2px 2px 5px #BABECC;
}
button:active{
  box-shadow: inset 1px 1px 2px #BABECC, inset -1px -1px 2px #FFF;
  outline:none;
}
button:focus{
  outline: none;
}
i{
  cursor: pointer;
}
</style>
