<template>
    <div class="app">
        <span class="close" @click="colseAddItem">✖</span>
        <div class="title">
            <label for="">title:</label>
            <input type="text" ref="title">
        </div>
        <div class="content">
            <label for="">content:</label><br>
            <textarea name="" id="" cols="60" rows="10" ref="content"></textarea>
        </div>
        <button class="submit" @click="submit">完成</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            todoData: {
                title: ``,
                content: ``
            }
        }
    },
    methods: {
        submit: function() {
            if(this.$refs.title.value == ``) {
                window.alert(`Please input title!`);
            }
            else if(this.$refs.content.value == ``) {
                window.alert(`Please input content!`);
            }
            else {
                this.todoData.title = this.$refs.title.value;
                this.todoData.content = this.$refs.content.value;
                this.$emit('submit',this.todoData);
            }
        },
        colseAddItem: function() {
            this.$emit('closeAddItem')
        }
    }
}
</script>

<style scoped>
.app {
    width: 500px;
    background-color: #ffffff;
    height: 250px;
    z-index: 999;
}
.title {
    width: 450px;
    margin: 0 auto;
}
.title input {
    width: 350px;
    border: 1px solid lightblue;
}
.content {
    width: 450px;
    margin: 0 auto;
}
.content textarea {
    border: 1px solid lightblue;
}
.submit {
    margin-left: 50%;
    transform: translateX(-50%);
}
.close {
    color: tomato;
    position: fixed;
    right: 10px;
    cursor: pointer;
}
</style>