<template>
  <div class="p-3 my-4 box__inner">
    <select
      :value="selectedSectionTitle"
      @change="sendSectionData"
      class="w-100">
      <option
        v-for="(section,index) in sections"
        :key="index"
        :value="index">{{section.sectionTitle}}</option>
    </select>
    <div class="my-3">
      <p class="mb-0">Section Name:</p>
      <p class="task__section-ttl">{{sections[selectedSectionTitle].sectionTitle}}</p>
      <textarea v-if="task.isEditable" v-model="task.text"></textarea>
      <p v-else>{{task.text}}</p>
      <div class="utilities d-flex justify-content-end">
        <i class="fas fa-save px-1"
          @click="$emit('edit',task)"></i>
        <i class="fas fa-check px-1"
          @click="$emit('check',task)"></i>
        <i
          class="fas fa-star px-1"
          :class="{star__yellow:task.favoriteTask}"
          @click="$emit('favorite',task)"
          ></i>
        <i class="fas fa-trash-alt px-1" @click="sendTask"></i>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props:["task","sectionId","sections","taskId"],
  data(){
    return {
      selectedSectionTitle: this.sectionId
    }
  },
  methods : {
    sendTask : function(){
      this.$emit("deleteTask",this.task);
    },
    sendSectionData : function(event){
      let location = event.target.value;
      this.$emit("transferSection",location,this.task);
    }
  }
}
</script>
<style>
.task__section-ttl{
  word-wrap: break-word
}
.task__ttl{
  border-radius: 4px;
  background-color: #E0E5EC;
  box-shadow: 2.25px 2.25px 4px rgb(163,177,198,0.6), -2.25px -2.25px 4px rgba(255,255,255, 0.5);
  min-height: 2rem;
}
.star__yellow{
  color: yellow;
}
</style>
