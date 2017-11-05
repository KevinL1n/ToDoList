<template>
  <div id='app'>
    <h1 v-html = 'title'></h1>
    <input v-model='newItem' v-on:keyup.enter='addNew' ></input>
    <ul>
      <li v-for='item in items' v-bind:class='{finished:item.isFinished}' v-on:click='toggleFinish(item)'>{{item.label}}</li>
    </ul>
  </div>
</template>

<script>
import Store from './store'
export default {
	el:'#app',
  data:function(){
    return {
      title:'This Is A Todolist',
      items:Store.fetch(),
      newItem:''
    }
  },
  watch:{
    items:{
      handler: function(items){
        Store.save(items)
      },
    deep:true
    }
  },
  methods:{
    toggleFinish: function(item){
      item.isFinished = !item.isFinished
    },
    addNew:function(){
      this.items.push({
        label:this.newItem,
       'isFinished':false 
      })
      this.newItem=''
    }
  }
}
</script>

<style>
*{margin: 0;padding: 0;}
.finished{
  text-decoration:underline;
  color: red;
}
li{
  list-style:none;
  font-size:1.6em;
  margin-top:10px;

}
#app {
 
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
input{
  width:230px;
  height:40px;
  border-radius:20px;
  padding: 0.4em 0.35em;
  border:3px solid deepskyblue;
  font-size: 1.55em;
}
</style>
