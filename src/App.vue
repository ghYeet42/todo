<script setup>

    import { ref, watch } from 'vue'

    let todos = ref(JSON.parse(window.localStorage.getItem('todos')) ?? [])

    let newTodo = ref('')

    let filter = ref('all')

    
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

    function todoFilter (todo) {
        if (filter.value == 'active') {
            return todo.complete == false
        } else if (filter.value == 'completed') {
            return todo.complete == true
        } else {
            return true
        }
    }

</script>



<template>

    <head>
        <link rel="stylesheet" ref="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    </head>

    <h1>My todo App!</h1>

        <input class="tabnav" type="radio" name="filter" value="all" v-model="filter">
        <label>All</label>

        <input class="tabnav" type="radio" name="filter" value="active" v-model="filter">
        <label>Active</label>

        <input class="tabnav" type="radio" name="filter" value="completed" v-model="filter">
        <label>Completed</label>

    <hr>

    <ul>

        <li v-for="(todo, index) in todos.filter(todoFilter)" :class="{completed: todo.complete}">

            <label class="container">
                <input type="checkbox" checked="checked" v-model="todo.complete">
                <span class="checkmark"></span>
            </label>
            
            <span id="todostxt">{{ todo.text }}</span>

            <br>

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
    background-color: #61F4F9;
    background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 2000 1500'%3E%3Cdefs%3E%3Crect fill='none' stroke-width='5.5' id='a' x='-400' y='-300' width='800' height='600'/%3E%3C/defs%3E%3Cg transform='scale(0.406)' style='transform-origin:center'%3E%3Cg transform='rotate(142.2 0 0)' style='transform-origin:center'%3E%3Cg transform='rotate(-160 0 0)' style='transform-origin:center'%3E%3Cg transform='translate(1000 750)'%3E%3Cuse stroke='%23E6FF7C' href='%23a' transform='rotate(10 0 0) scale(1.1)'/%3E%3Cuse stroke='%23f6f067' href='%23a' transform='rotate(20 0 0) scale(1.2)'/%3E%3Cuse stroke='%23ffdf58' href='%23a' transform='rotate(30 0 0) scale(1.3)'/%3E%3Cuse stroke='%23ffcd50' href='%23a' transform='rotate(40 0 0) scale(1.4)'/%3E%3Cuse stroke='%23ffba4f' href='%23a' transform='rotate(50 0 0) scale(1.5)'/%3E%3Cuse stroke='%23ffa755' href='%23a' transform='rotate(60 0 0) scale(1.6)'/%3E%3Cuse stroke='%23ff9260' href='%23a' transform='rotate(70 0 0) scale(1.7)'/%3E%3Cuse stroke='%23ff7d6e' href='%23a' transform='rotate(80 0 0) scale(1.8)'/%3E%3Cuse stroke='%23ff687f' href='%23a' transform='rotate(90 0 0) scale(1.9)'/%3E%3Cuse stroke='%23ff5692' href='%23a' transform='rotate(100 0 0) scale(2)'/%3E%3Cuse stroke='%23ff48a6' href='%23a' transform='rotate(110 0 0) scale(2.1)'/%3E%3Cuse stroke='%23ff41bb' href='%23a' transform='rotate(120 0 0) scale(2.2)'/%3E%3Cuse stroke='%23ef44d0' href='%23a' transform='rotate(130 0 0) scale(2.3)'/%3E%3Cuse stroke='%23ce4de2' href='%23a' transform='rotate(140 0 0) scale(2.4)'/%3E%3Cuse stroke='%23a257f3' href='%23a' transform='rotate(150 0 0) scale(2.5)'/%3E%3Cuse stroke='%236061FF' href='%23a' transform='rotate(160 0 0) scale(2.6)'/%3E%3C/g%3E%3C/g%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
    background-attachment: fixed;
    background-size: cover;
}

h1 {
    text-align: center;
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
    text-decoration: underline;
}

#tdta {
    margin: 0;
    position: relative;
    -ms-transform: translate(-50%, -50%);
    transform: translate(-50%, -50%);
    left: 50%;
    padding: 10px 25px;
}

#todostxt {
    position: absolute;
    left: 7%;
}

.completed {
    text-decoration: line-through;
    background-color:bisque;
}

li {
    text-align: center;
}

button {
    position: absolute;
    right: 2%;
}

/* The container */
.container {
  display: block;
  position: relative;
  padding-left: 35px;
  margin-bottom: 12px;
  cursor: pointer;
  font-size: 22px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/* Hide the browser's default checkbox */
.container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

/* Create a custom checkbox */
.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 25px;
  width: 25px;
  background-color: #eee;
  padding: 10px 10px 10px 10px;
}

/* On mouse-over, add a grey background color */
.container:hover input ~ .checkmark {
  background-color: #ccc;
}

/* When the checkbox is checked, add a blue background */
.container input:checked ~ .checkmark {
  background-color: #2196F3;
}

/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

/* Show the checkmark when checked */
.container input:checked ~ .checkmark:after {
  display: block;
}

/* Style the checkmark/indicator */
.container .checkmark:after {
  left: 9px;
  top: 5px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}

/* 

input[type="checkbox"]:after {
    font-family: "Font Awesome 6 Free";
    content: "/";
    font-weight: 500;
}

input[type="checkbox"]:hover {

}


input[type="checkbox"]:checked:after {
    display: block;
}


for tdta {
    -ms-transform: translate(-50%, -50%);
    transform: translate(-50%, -50%);
}


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