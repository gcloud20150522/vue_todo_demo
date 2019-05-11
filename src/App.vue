<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <TodoHeader :addItem="addItem"/>
        <TodoList :todos="todos" :removeTodo="removeTodo"/>
        <TodoFooter :todos="todos" :removeCompleted="removeCompleted" :selectAll="selectAll"/>
      </div>
    </div>
  </div>
</template>

<script>
import TodoHeader from './components/todoHeader'
import TodoList from './components/todoList'
import TodoFooter from './components/todoFooter'


export default {
  name: 'App',
  components: {
    TodoHeader,TodoList,TodoFooter
  },
  data(){
    return{
      todos:[],
    }
  },
  methods:{
    addItem(todo){
      this.todos.unshift(todo)
    },
    removeTodo(index){
      this.todos.splice(index,1)
    },
    removeCompleted(){
      this.todos=this.todos.filter(todo=>{
        return todo.completed==false;
      })
    },
    selectAll(isCheck){
      if(isCheck){
        this.todos=this.todos.map(todo=>{
        return {title:todo.title,completed:true};
      });
      }else{
        this.todos=this.todos.map(todo=>{
        return {title:todo.title,completed:false};
      });
      }
    }
    

  },
  watch:{
    todos:{
      deep:true,
      handler:function(value,oldvalue){
        localStorage.setItem('todo_data',JSON.stringify(value));
      }

    }
  },
  mounted(){
    this.todos=JSON.parse(localStorage.getItem('todo_data'));
  }
  
}
</script>

<style>
  /*app*/
.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>
