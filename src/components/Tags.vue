<template>
<div class="tag-container">
    <Tag 
    v-for="(tag, index) in tags" 
    :tag="tag"
    :index="index"
    @removeOneTagEvent="removeOneTag($event)"
    />
    <input 
    type="text" 
    @keydown.enter="addTag"
    @keydown.backspace="removeTag" />

    <div class="error" v-if="error">Bu etiket eklenmiş!</div>
</div>
</template>
<script>
import Tag from "./Tag"
export default {
    components:{
        Tag
    },
    data(){
    return{
        tags:[],
        error: false
    }
  },
  methods:{
    addTag(event){
      let text = event.target;
      let matchTag = false
      if(text.value.length > 0){

        this.tags.forEach(tag => {
          if(tag.toLowerCase() === text.value.toLowerCase()){
            matchTag = true
          }
        })

        if(!matchTag){
          this.tags.push(text.value);
          text.value = '';
        }
        else{
          this.error = true;
          setTimeout(()=>{
            this.error = false;
          },2000)
        }
      }
    },
    removeTag(e){
      if(e.target.value.length <= 0)
      {
       this.tags.splice(this.tags.length -1, 1)
      }
    },
    removeOneTag(index){
      this.tags.splice(index, 1)
    }
  },
  props:{
    value :{
      require: false
    }
  },
  created(){
    if(this.value){
      if(this.value.length > 0){
        this.tags = this.value.split(",")
      }
    }
  }
}
</script>
<style scoped>
  .tag-container{
    border:1px solid #ccc;
    padding:20px;
  }
 

  input{
    outline: nnone;
    width: 100px;
    height:30px;
  }
  .error{
    font-size:12px;
    color:red;
    margin-top:15px;
  }
</style>