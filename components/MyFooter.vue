<template>
  <div class="todo-footer" v-show="total">
    <label>
      <input type="checkbox" v-model="isAll"/>
    </label>
    <span> <span>已完成{{undone}}</span> / {{total}} </span>
    <button class="btn btn-danger" @click="clearAllTodo">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: "MyFooter",
  props:['todos','checkAllTodo','clearAllTodo'],
  computed:{
    total(){
      return this.todos.length
    },
    undone(){
      // 1,过滤
      // let n=0;
      // this.todos.forEach(el => {
      //   if(el.done)n++
      // });
      // return n
      
      // 2.统计
      // const x = this.todos.reduce((premtodo)=>{
      //   return pre + (todo.done ? 1: 0)
      // },0)
      // console.log(x);

      // 3.统计-简写
      return this.todos.reduce((pre,todo)=> pre + (todo.done ? 1: 0),0)
    },
    isAll:{
      get(){
        return this.undone==this.total
      },
      set(v){
        this.checkAllTodo(v);
      }
    }
  }
};
</script>

<style scoped>
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