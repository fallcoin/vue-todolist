<template>
    <div class="app">
        <div class="top">
            <div @click="changeCompletedStatus" :class="currentTodo.completed ? `status-completed` : ``" class="status"></div>
            <label class="title" @click="changeContentStatus" :class="currentTodo.completed ? `title-completed` : ``">{{currentTodo.title}}</label>
            <div class="delete" @click="deleteTodo">✖</div>
        </div>
        <div :class="status">
            <div class="content" ref="content">{{currentTodo.content}}</div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            status: `fold`,
            contentHeight: 0
        }
    },
    props: {
        currentTodo: {
            type: Object,
            required: true
        }
    },
    computed: {
    },
    methods: {
        changeContentStatus: function() {
            this.status == `fold` ? this.status = `` : this.status = `fold`;
        },
        changeCompletedStatus: function() {
            this.currentTodo.completed = !this.currentTodo.completed;
        },
        deleteTodo: function() {
            this.$emit(`deleteTodo`,this.currentTodo.id);
        }
    },
    mounted: function() {
        this.contentHeight = this.$refs.content.offsetHeight;
    }
}
</script>

<style scoped>
.app {
    width: 600px;
    border-top: 1px solid lightblue;
    font-size: 20px;
}
.top {
    width: 600px;
    display: flex;
}
.status {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    border: 1px solid cornflowerblue;
    margin-left: 10px;
    margin-right: 10px;
    margin-top: 1px;
    cursor: pointer;
}
.title {
    width: 520px;
    margin-right: 20px;
    cursor: pointer;
}
.delete {
    cursor: pointer;
    color: tomato;
}
.content {
    width: 600px;
    overflow: hidden;
}
.fold {
    width: 600px;
    overflow: hidden;
    height: 0;
}
.title-completed {
    text-decoration: line-through;
}
.status-completed {
    background-color: cornflowerblue;
}
</style>