<script setup>

    import { ref, watch } from 'vue'

    let todos = ref(JSON.parse(window.localStorage.getItem('todos')))

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

    <h1>My todo App!</h1>

    <ul>

        <li v-for="(todo, index) in todos">

            <input type="checkbox" id="check" checked="checked" v-model="todo.complete"><button @click="deleteTodo(index)">X</button>

            {{ todo.text }}

        </li>
        
    </ul>

    <input v-model="newTodo" type="text" id="tdta" @keydown.enter="addTodo">
    <button @click="addTodo">Add todo</button>

</template>



<style>

body {
    color: white;
    background-color: black;
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

.check {
  height: 25px;
  width: 25px;
  background-color: rgb(175, 0, 0);
}

.checked {
  background-color: #000000;
}


.check:after {
  content: "";
  position: absolute;
  display: none;
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