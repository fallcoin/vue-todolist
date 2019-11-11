<template>
    <div class="container">
        <div class="todoItemCount">
            <span>{{caculateCount}}</span>
        </div>
        <div class="bar">
            <span v-for="(tabName) in tabBar" :key="tabName" class="close" :class="[filter == tabName ? `on` : ``]" @click="toggleFilter">{{tabName}}</span>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            tabBar: [`All`,`Todo`,`Finish`]
        }
    },
    props: {
        filter: {
            type: String,
            require: true
        },
        count: {
            type: Number,
            require: true
        }
    },
    computed: {
        caculateCount: function() {
            return `${this.count} items to do`
        }
    },
    methods: {
        toggleFilter: function(event) {
            return this.$emit(`toggleFilter`,event.target.innerText);
        }
    }
}
</script>

<style scoped>
.container {
    width: 600px;
    display: flex;
    justify-content: space-between;
}
.bar {
    display: flex;
    width: 400px;
    justify-content: space-around;
}
.close {
    cursor: pointer;
    font-size: 20px;
    color: #0984e3;
}
.on {
    color: tomato;
}
.todoItemCount {
    margin-left: 10px;
    line-height: 28px;
    color: yellowgreen;
}
</style>