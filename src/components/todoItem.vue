<template>
    <li @mouseenter="enter" @mouseleave="out" ref="ref1">
      <label>
        <input type="checkbox" v-model="todo.completed"/>
        <span>{{todo.title}}</span>
      </label>
      <button class="btn btn-danger" v-show="isShow" @click='remove(index)'>删除</button>
    </li>
</template>

<script>
  export default {
    props:{
      todo:Object,
      index:Number,
      removeTodo:Function
    },
    data(){
      return{
        isShow:false,
      }
    },
    methods:{
      enter(){
        this.$refs.ref1.style.background="pink";
        this.isShow=true;
      },
      out(){
        this.$refs.ref1.style.background="";
        this.isShow=false;
      },
      remove(index){
        if(window.confirm(`确认删除任务:'${this.todo.title}'吗？`)){
          this.removeTodo(index)
        }
        
      }
      
    },
  }
</script>

<style>
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}
</style>
