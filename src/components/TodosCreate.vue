<script setup>
import { defineEmits, reactive, watch } from 'vue';
import TodoButton from './TodoButton.vue'
const emit = defineEmits(["create-todo"])

const todoState = reactive({
    todo: "",
    invalid: false,
    errMsg: "Todo value can't be empty"
})

const createTodo = () => {
    todoState.invalid = false
    if (todoState.todo !== "") {
        emit("create-todo", todoState.todo)
        todoState.todo = "";
        return;
    }
    todoState.invalid = true;
    todoState.errMsg = "Todo value can't be empty"
}

</script>

<template>
    <div class="input-wrap" :class="{ 'input-err': todoState.invalid }">
        <input type="text" placeholder="Create todo" v-model="todoState.todo" />
        <TodoButton @click="createTodo()" >Create</TodoButton>
    </div>
    <p v-show="todoState.invalid" class="err-msg">{{ todoState.errMsg }}</p>
</template>



<style lang="scss" scoped>
.input-wrap {
    display: flex;
    height: 50px;
    border-radius: 5px;
    overflow: hidden;
    transition: 250ms ease;
    border: 2px solid #41b080;

    &.input-err {
        border: 2px solid red;
    }

    &:focus-within {
        box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
            0 -2px 4px -2px rgb(0 0 0 / 0.1);
    }

    input {
        width: 100%;
        padding: 8px 6px;
        border: none;

        &:focus {
            outline: none;
        }
    }


}

.err-msg {
    color: red;
    text-align: center;
    padding: 5px
}
</style>