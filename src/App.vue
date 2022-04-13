<template>
  <div class="container">
    <app-tags v-model="tags" :value="tags"/>
    {{tags}}
    <app-tags v-model="tags2" :value="tags2"/>
    {{tags2}}
  </div>
</template>
<script>
import Tags from "./components/Tags"
export default{
  components:{
    appTags: Tags
  },
  data(){
    return{
      tags:"deneme,test,haktan",
      tags2:"deneme,test,haktan,klavye"
    }
  }
}
</script>
<style>
  body{
    font-family: sans-serif;
  }

  
 
</style>