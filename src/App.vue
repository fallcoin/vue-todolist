<template>
  <div class="app">
    <Header class="header"/>
    <Todo :todoList="todoList"/>
    <SideBar class="sideBar" @showAddItem="showAddItem" @clearAll="clearAll"/>
    <AddItem v-if="status" class="addItem" @submit="submit" @closeAddItem="closeAddItem"/>
    <div v-bind:class="status"></div>
  </div>
</template>

<script>
import SideBar from "./components/sideBar.vue";
import Header from "./components/header.vue";
import Todo from "./components/todo";
import AddItem from "./components/addItem";

export default {
  data() {
    return {
      status: ``,
      todoList: [],
      id: 0
    };
  },
  components: {
    SideBar,
    Header,
    Todo,
    AddItem
  },
  methods: {
    showAddItem() {
      this.status = `addTodo`
    },
    submit(todoData) {
      todoData.id = ++this.id;
      this.todoList.unshift({
        id: todoData.id,
        title: todoData.title.trim(),
        content: todoData.content,
        completed: false
      });
      this.status = ``;
    },
    clearAll() {
      if(this.todoList)
        window.alert("您还未添加任何数据");
      else
        if(window.confirm("确定清空所有吗？"))
          this.todoList.splice(0,this.todoList.length);
    },
    closeAddItem() {
      this.status = ``;
    }
  }
}
</script>

<style scoped>
.app {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
}
.addTodo {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  z-index: 1;
  opacity: 0.9;
  background-color: #999;
}
.header {
  margin-top: 40px;
}
.sideBar {
  position: fixed;
  right: 40px;
  top: 40px;
}
.addItem {
  position: fixed;
  left: 50%;
  top: 50%;
  transform: translate(-50%,-50%);
}
</style>
