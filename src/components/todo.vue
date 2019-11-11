<template>
    <div class="todo">
        <Tab :filter='state' @toggleFilter="toggleFilter" :count="calculateTodo"/>
        <div>
            <Item v-for="todo in showTodoList" :key="todo.id" :currentTodo="todo" @deleteTodo="deleteTodo"/>
            <div v-show="!todoList.length" class="tip">
                <span>您还未添加任何事件</span>
            </div>
        </div>
    </div>
</template>

<script>
import Tab from "./tab";
import Item from "./item";
export default {
    data() {
        return {
            showTodoList: [],
            state: `All`
        }
    },
    props: ['todoList'],
    components: {
        Tab,
        Item
    },
    computed: {
        calculateTodo: function() {
            return this.todoList.filter(current => current.completed === false).length;
        }
    },
    methods: {
        toggleFilter: function(nextState) {
            this.state = nextState;
            this.changeShowTodoList();
        },
        changeShowTodoList: function() {
            if(this.state === `Todo`)
                this.showTodoList = this.todoList.filter(current => current.completed == false);
            else if(this.state === `Finish`)
                this.showTodoList = this.todoList.filter(current => current.completed == true);
            else
                this.showTodoList = this.todoList;
        },
        deleteTodo: function(id) {
            this.todoList.splice(this.todoList.findIndex(current => current.id == id),1);
        }
    },
    mounted() {
        this.changeShowTodoList();
    }
}
</script>

<style scoped>
.todo {
    background-color: #fff;
    width: 600px;
    margin-left: 50%;
    transform: translateX(-50%);
}
.tip {
    color: tomato;
    text-align: center;
    font-size: 20px;
}
</style>