<template>
     <HeaderTitle />
     <AddTodo v-on:add-todo="addTodo" />
   <todos v-bind:todos="todos" v-on:del-todo="deletetodo"/>
     
   
</template>

<script>
 import axios from 'axios';
import todos from './components/todos';
import HeaderTitle from './components/layouts/header';
import  AddTodo from './components/AddTodo';
export default {
  name: 'App',
  components: { 
    HeaderTitle,
    todos,
    AddTodo
    
} ,

 data(){
   return {
     todos:  []
   }
 },
 methods:{
   deletetodo(id){
     axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(res => this.todos = this.todos.filter(todo => todo.id !== id, res.data))
     .catch(err =>console.log(err));
     
   },

    addTodo(newTodo){
      const { title,completed } = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos',
      {title , completed
      })
      .then(res =>  this.todos =[...this.todos,res.data])
      .catch()
   }
 },
 created(){
            axios.get("https://jsonplaceholder.typicode.com/todos?_limit=5")
            .then(res => this.todos = res.data)
            .catch(err => console.log(err)) 
 }
  
   
}
</script>

<style>

*{
  box-sizing:border-box;
  margin:0;
  padding:0;
} 

 body{
   font-family: Arial, Helvetica, sans-serif;
   line-height: 1.4;
 }

 .btn{
      display:inline-block;
      border:none;
      background:#555;
      color:#fff;
      padding:7px 20px;
      cursor:pointer;
 }

 .btn:hover {
   background:#666;
 }
 

</style>
  