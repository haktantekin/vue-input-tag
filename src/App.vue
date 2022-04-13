<template>
  <div class="tag-container">
    <span class="tag" v-for="(tag, index) in tags">
      <span class="content">{{tag}}</span>
      <span class="close" @click="removeOneTag(index)">x</span>
    </span>
    <input 
    type="text" 
    @keydown.enter="addTag"
    @keydown.backspace="removeTag">

    <div class="error" v-if="error">Bu etiket eklenmiş!</div>
  </div>
</template>
<script>
export default{
  data(){
    return{
      tags:["deneme","test"],
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
  }
}
</script>
<style>
  body{
    font-family: sans-serif;
  }
  .tag-container{
    border:1px solid #ccc;
    padding:20px;
  }
  .tag{
    background: #fbbd08;
    padding: 10px;
    color:#000;
    cursor: default;
    font-size:14px;
    margin-right:10px;
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
  
  .tag .close{
    font-size:12px;
    cursor: pointer;
  }
</style>