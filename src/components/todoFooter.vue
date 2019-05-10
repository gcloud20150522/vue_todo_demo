<template>
  <div class="todo-footer">
    <label>
      <input type="checkbox" v-model="check"/>
    </label>
    <span>
      <span>已完成{{ completed }}</span> / 全部{{todos.length}}
    </span>
    <!-- //completed等于0时隐藏该按钮 -->
    <button class="btn btn-danger" @click="removeCompleted" v-show="completed">清除已完成任务</button>
  </div>
</template>

<script>
export default {
 props:{
   todos:Array,
   removeCompleted:Function,
   selectAll:Function,
 },
 data(){
   return{
     isCheck:false,
   }
 },
  computed:{
    //key1:已经完成任务的计算属性
    completed(){
      //key2:数组的reduce方法
      return this.todos.reduce((pretatal,todo)=>{
        return pretatal+(todo.completed==true?1:0)
      },0)
    },
    check:{
      // get:function(){
      //   let istrue;
      //   this.todos.forEach(item=>{
      //     if(item.completed==false){
      //       istrue=false;
      //       return;
      //     }else{
      //       istrue=true;
      //     }
      //   });
      //   return istrue;
      
      // },
      //key3:已经完成任务等于todos.length,触发check属性的get方法
      get(){
        return this.completed==this.todos.length && this.todos.length!=0;
      },
      set(isCheck){
        this.selectAll(isCheck)
      }
    }
  },
 
//  mounted(){
//    console.log(this.selectAll);
//  }
}
</script>

<style>
/*footer*/
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}

</style>
