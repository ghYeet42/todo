<script setup>

    import { ref, watch } from 'vue'

    let todos = ref(JSON.parse(window.localStorage.getItem('todos')) ?? [])

    let newTodo = ref('')

    
    watch (todos, function(value) {
        window.localStorage.setItem('todos', JSON.stringify(value))
    }, {deep: true})


    function addTodo () {
        todos.value.push({
            text: newTodo.value, 
            complete: false
        })

        newTodo.value = ''
    }

    function deleteTodo (index) {
        todos.value.splice (index, 1)
    }

</script>



<template>

    <head>
        <link rel="stylesheet" ref="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    </head>

    <h1>My todo App!</h1>

    <ul>

        <li v-for="(todo, index) in todos" :class="{completed: todo.complete}">

            <input type="checkbox" id="checkbox" checked="checked" class v-model="todo.complete">

            {{ todo.text }}

            <button @click="deleteTodo(index)">x</button>

        </li>
        
    </ul>

    <input v-model="newTodo" type="text" id="tdta" @keydown.enter="addTodo">
    <button @click="addTodo">Add todo</button>

</template>



<style>

body {
    color: rgb(0, 0, 0);
    background-color: rgb(255, 255, 255);
}

h1 {
    text-align: center;
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
    text-decoration: underline;
}

#tdta {
    margin: 0;
    position: absolute;
    top: 35%;
    left: 50%;
    -ms-transform: translate(-50%, -50%);
    transform: translate(-50%, -50%);
    padding: 10px 25px;
}

.completed {
    text-decoration: line-through;
    background-color:bisque;
}

input [type="checkbox"] {
    height: 100px;
    width: 100px;
    background-color: rgb(0, 0, 0);
    cursor: pointer;
    font-size: 200px;
}

li {
    text-align: center;
}

input [type="checkbox"]:after {
    font-family: "Font Awesome 6 Free";
    content: "/f772";
    font-weight: 500;
}

input [type="checkbox"]:hover {

}


input [type="checkbox"]:checked:after {
    display: block;
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