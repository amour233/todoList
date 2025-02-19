<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <MyHeader :receive="receive" />
      <MyList :todos="todos" :handleChange="handleChange" :handleDelete="handleDelete"/>
      <MyFooter :todos="todos" :checkAllTodo="checkAllTodo" :clearAllTodo="clearAllTodo"/>
    </div>
  </div>
</template>

<script>
import MyHeader from "./components/MyHeader.vue";
import MyFooter from "./components/MyFooter.vue";
import MyList from "./components/MyList.vue";

export default {
name: "App",
components: {
  MyHeader,
  MyFooter,
  MyList,
},
data() {
  return {
    todos: JSON.parse(localStorage.getItem("todos")) ? JSON.parse(localStorage.getItem("todos")) : []
  }
},
watch:{
  todos:{
    deep:true,
    handler(v){
      localStorage.setItem("todos",JSON.stringify(v))
    }
  }
},
methods:{
  // 添加一个todo
  receive(obj){
    this.todos.unshift(obj);
  },
  // 勾选or取消勾选一个todo
  handleChange(id){
    this.todos.forEach((el)=>{
      if(el.id==id)el.done=!el.done;
    })
  },
  // 删除一个todo
  handleDelete(id){
    this.todos = this.todos.filter(el=>el.id!==id)
  },
  // 全选or取消全选
  checkAllTodo(v){
    this.todos.forEach((el)=>{
      el.done=v
    })
  },
  // 清除所有已经完成的todo
  clearAllTodo(){
    this.todos=this.todos.filter((el)=>{
      return !el.done
    })
  }
}
};
</script>

<style>
/*base*/
body {
background: #fff;
}

.btn {
display: inline-block;
padding: 4px 12px;
margin-bottom: 0;
font-size: 14px;
line-height: 20px;
text-align: center;
vertical-align: middle;
cursor: pointer;
box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
  0 1px 2px rgba(0, 0, 0, 0.05);
border-radius: 4px;
}

.btn-danger {
color: #fff;
background-color: #da4f49;
border: 1px solid #bd362f;
}

.btn-danger:hover {
color: #fff;
background-color: #bd362f;
}

.btn:focus {
outline: none;
}

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