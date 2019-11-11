<template>
    <div class="container">
        <div v-for="tab in tabList" :key="tab.text" @click="doSomething(tab.method)" class="sideBarItem">
            <span>{{tab.text}}</span>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            tabList: [{
                text: `clear`,
                method: `delete`
            },{
                text: `add`,
                method: `addItem`
            }]
        }
    },
    computed: {
    },
    methods: {
        doSomething: function(func) {
            return this[func]();
        },
        delete: function() {
            this.$emit(`clearAll`)
        },
        addItem: function () {
            this.$emit('showAddItem');
        }
    }
}
</script>

<style scoped>
.container {
    display: flex;
}
.sideBarItem {
    background-color: #fff;
    margin-left: 10px;
    width: 50px;
    height: 50px;
    border-radius: 50%;
    text-align: center;
    line-height: 50px;
    cursor: pointer;
}
</style>