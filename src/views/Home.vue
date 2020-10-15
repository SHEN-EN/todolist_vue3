<template>
<div>
    <div>
        <h1>已完成</h1>
        <li v-for="(item,index) in isTodo" :key="index">
            {{item}}
            <input type="checkbox">
        </li>
    </div>
    <div>
        <h1>未完成</h1>
        <li v-for="(item,index) in noTodo" :key="index">
            {{item}}
            <input type="checkbox" @change="changes(index)">
        </li>

    </div>
    <div>
        <h1>新增代办</h1>
        <button @click="add">新增</button>
        <li></li>
    </div>
    <div>{{total}}</div>
</div>
</template>

<script>
import {
    reactive,
    toRefs,
    watchEffect,
    computed
} from 'vue'

export default {
    setup() {
        const state = reactive({
            isTodo: [],
            noTodo: [],
            a: 0
        });
        const add = () => {
            state.noTodo.push('1');
            state.a++
        };
        const changes = (index) => {
            let noTodo = state.noTodo.splice(index, 1);
            state.isTodo.push(noTodo[0]);
        };
        watchEffect(() => {
            console.log(state.a)
        });
        const total = computed(() => {
            return state.a + 2
        })
        return {
            ...toRefs(state),
            add,
            changes,
            total
        }
    }
}
</script>

<style lang="">

</style>
