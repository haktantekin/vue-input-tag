<template>
  <div class="tag-container">
    <span class="tag" v-for="tag in tags">
      <span class="content">{{tag}}</span>
      <span class="close">x</span>
    </span>
    <input type="text" @keydown.enter="addTag">
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
      let text = event.target.value;
      let matchTag = false
      if(text.length > 0){

        this.tags.forEach(tag => {
          if(tag.toLowerCase() === text.toLowerCase()){
            matchTag = true
          }
        })

        if(!matchTag){
          this.tags.push(text);
          text = '';
        }
        else{
          this.error = true;
          setTimeout(()=>{
            this.error = false;
          },2000)
        }
      }
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