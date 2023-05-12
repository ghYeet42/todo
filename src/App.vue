<script setup>

    import { ref } from 'vue'

    let todos = ref([])

    let person = {
        text: " ",
        lastName: false,
        id: 5566,
        fullName : function() {
            return this.firstName + " " + this.lastName;
        }
    };

    let newTodo = ref('')

    function addTodo () {
        todos.value.push({
            text: newTodo.value, 
            completed: false
        })

        newTodo.value = ''
    }

    function deleteTodo (index) {
        todos.value.splice (index, 1)
    }

</script>



<template>

    <h1>My todo App!</h1>

    <ul>

        <li v-for="(todo, index) in todos">

            <input type="checkbox" v-model="todo.completed">

            {{ todo.text }}

            <button @click="deleteTodo(index)">X</button>

        </li>
        
    </ul>

    <input v-model="newTodo" type="text" @keydown.enter="addTodo">
    <button @click="addTodo">Add todo</button>

</template>



<style>

h1 {
    text-align: center;
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
    text-decoration: underline;
}

input {
    margin: 0;
    position: absolute;
    top: 35%;
    left: 50%;
    -ms-transform: translate(-50%, -50%);
    transform: translate(-50%, -50%);
    padding: 10px 25px;
}

/* 

ul {
    text-align: center;
    list-style-type: none;
    margin: 0;
    padding: 0;
    position: relative;
}

input {
    margin: 0;
    position: absolute;
    top: 35%;
    left: 50%;
    -ms-transform: translate(-50%, -50%);
    transform: translate(-50%, -50%);
    padding: 15px 32px;
}

button {
    margin: 0;
    position: absolute;
    top: 70%;
    left: 30%;
    -ms-transform: translate(-50%, -50%);
    transform: translate(-50%, -50%);
    padding: 15px 32px;
}

*/

</style>