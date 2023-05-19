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

    function activeFilter (todo) {
        return todo.complete == false
    }

    function clearCompleted () {
        todos.value = []
    }

</script>



<template>

    <h1>My todo App!</h1>

    <p>{{ todos.filter(activeFilter).length }} items left</p>

    <div>

        <label class="container">All
        <input type="radio" name="filter" value="all" v-model="filter">
        <span class="checkmark2"></span>
        </label>

        <label class="container">Active
        <input type="radio" name="filter" value="active" v-model="filter">
        <span class="checkmark2"></span>
        </label>


        <label class="container">Completed
        <input type="radio" name="filter" value="completed" v-model="filter">
        <span class="checkmark2"></span>
        </label>

        <label class="container">
        <button @click="clearCompleted">Clear Completed</button>
        </label>

    </div>

    <br>

    <hr>

    <br>
    <br>
    <br>
    <br>

    <div class="todobox">

        <input v-model="newTodo" type="text" id="tdta" placeholder="Press enter to add to your list!" @keydown.enter="addTodo">

        <ul>

            <li v-for="(todo, index) in todos.filter(todoFilter)" :class="{completed: todo.complete}" class="deletion">

                <label class="container">
                    <input type="checkbox" checked="checked" v-model="todo.complete">
                    <span class="checkmark"></span>
                </label>
                
                <br><span id="todostxt">{{ todo.text }}</span>

                <br>

                <button class="delete" @click="deleteTodo(index)">x</button>

            </li>
            
        </ul>

        <br>
        <br>
        <br>
        <br>

        <button @click="addTodo" class="addbutton">Add todo</button>

    </div>

</template>



<style>

body {
    color: #eee;
    background-color: #292A2C;
    background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 2000 1500'%3E%3Cdefs%3E%3Crect stroke='%23292A2C' stroke-width='0.4' width='1' height='1' id='s'/%3E%3Cpattern id='a' width='3' height='3' patternUnits='userSpaceOnUse' patternTransform='rotate(18 1000 750) scale(10.85) translate(-907.83 -680.88)'%3E%3Cuse fill='%23363739' href='%23s' y='2'/%3E%3Cuse fill='%23363739' href='%23s' x='1' y='2'/%3E%3Cuse fill='%23414243' href='%23s' x='2' y='2'/%3E%3Cuse fill='%23414243' href='%23s'/%3E%3Cuse fill='%234a4b4c' href='%23s' x='2'/%3E%3Cuse fill='%234a4b4c' href='%23s' x='1' y='1'/%3E%3C/pattern%3E%3Cpattern id='b' width='7' height='11' patternUnits='userSpaceOnUse' patternTransform='rotate(18 1000 750) scale(10.85) translate(-907.83 -680.88)'%3E%3Cg fill='%23525354'%3E%3Cuse href='%23s'/%3E%3Cuse href='%23s' y='5' /%3E%3Cuse href='%23s' x='1' y='10'/%3E%3Cuse href='%23s' x='2' y='1'/%3E%3Cuse href='%23s' x='2' y='4'/%3E%3Cuse href='%23s' x='3' y='8'/%3E%3Cuse href='%23s' x='4' y='3'/%3E%3Cuse href='%23s' x='4' y='7'/%3E%3Cuse href='%23s' x='5' y='2'/%3E%3Cuse href='%23s' x='5' y='6'/%3E%3Cuse href='%23s' x='6' y='9'/%3E%3C/g%3E%3C/pattern%3E%3Cpattern id='h' width='5' height='13' patternUnits='userSpaceOnUse' patternTransform='rotate(18 1000 750) scale(10.85) translate(-907.83 -680.88)'%3E%3Cg fill='%23525354'%3E%3Cuse href='%23s' y='5'/%3E%3Cuse href='%23s' y='8'/%3E%3Cuse href='%23s' x='1' y='1'/%3E%3Cuse href='%23s' x='1' y='9'/%3E%3Cuse href='%23s' x='1' y='12'/%3E%3Cuse href='%23s' x='2'/%3E%3Cuse href='%23s' x='2' y='4'/%3E%3Cuse href='%23s' x='3' y='2'/%3E%3Cuse href='%23s' x='3' y='6'/%3E%3Cuse href='%23s' x='3' y='11'/%3E%3Cuse href='%23s' x='4' y='3'/%3E%3Cuse href='%23s' x='4' y='7'/%3E%3Cuse href='%23s' x='4' y='10'/%3E%3C/g%3E%3C/pattern%3E%3Cpattern id='c' width='17' height='13' patternUnits='userSpaceOnUse' patternTransform='rotate(18 1000 750) scale(10.85) translate(-907.83 -680.88)'%3E%3Cg fill='%235a5a5b'%3E%3Cuse href='%23s' y='11'/%3E%3Cuse href='%23s' x='2' y='9'/%3E%3Cuse href='%23s' x='5' y='12'/%3E%3Cuse href='%23s' x='9' y='4'/%3E%3Cuse href='%23s' x='12' y='1'/%3E%3Cuse href='%23s' x='16' y='6'/%3E%3C/g%3E%3C/pattern%3E%3Cpattern id='d' width='19' height='17' patternUnits='userSpaceOnUse' patternTransform='rotate(18 1000 750) scale(10.85) translate(-907.83 -680.88)'%3E%3Cg fill='%23292A2C'%3E%3Cuse href='%23s' y='9'/%3E%3Cuse href='%23s' x='16' y='5'/%3E%3Cuse href='%23s' x='14' y='2'/%3E%3Cuse href='%23s' x='11' y='11'/%3E%3Cuse href='%23s' x='6' y='14'/%3E%3C/g%3E%3Cg fill='%23606162'%3E%3Cuse href='%23s' x='3' y='13'/%3E%3Cuse href='%23s' x='9' y='7'/%3E%3Cuse href='%23s' x='13' y='10'/%3E%3Cuse href='%23s' x='15' y='4'/%3E%3Cuse href='%23s' x='18' y='1'/%3E%3C/g%3E%3C/pattern%3E%3Cpattern id='e' width='47' height='53' patternUnits='userSpaceOnUse' patternTransform='rotate(18 1000 750) scale(10.85) translate(-907.83 -680.88)'%3E%3Cg fill='%23FFFFFF'%3E%3Cuse href='%23s' x='2' y='5'/%3E%3Cuse href='%23s' x='16' y='38'/%3E%3Cuse href='%23s' x='46' y='42'/%3E%3Cuse href='%23s' x='29' y='20'/%3E%3C/g%3E%3C/pattern%3E%3Cpattern id='f' width='59' height='71' patternUnits='userSpaceOnUse' patternTransform='rotate(18 1000 750) scale(10.85) translate(-907.83 -680.88)'%3E%3Cg fill='%23FFFFFF'%3E%3Cuse href='%23s' x='33' y='13'/%3E%3Cuse href='%23s' x='27' y='54'/%3E%3Cuse href='%23s' x='55' y='55'/%3E%3C/g%3E%3C/pattern%3E%3Cpattern id='g' width='139' height='97' patternUnits='userSpaceOnUse' patternTransform='rotate(18 1000 750) scale(10.85) translate(-907.83 -680.88)'%3E%3Cg fill='%23FFFFFF'%3E%3Cuse href='%23s' x='11' y='8'/%3E%3Cuse href='%23s' x='51' y='13'/%3E%3Cuse href='%23s' x='17' y='73'/%3E%3Cuse href='%23s' x='99' y='57'/%3E%3C/g%3E%3C/pattern%3E%3C/defs%3E%3Crect fill='url(%23a)' width='100%25' height='100%25'/%3E%3Crect fill='url(%23b)' width='100%25' height='100%25'/%3E%3Crect fill='url(%23h)' width='100%25' height='100%25'/%3E%3Crect fill='url(%23c)' width='100%25' height='100%25'/%3E%3Crect fill='url(%23d)' width='100%25' height='100%25'/%3E%3Crect fill='url(%23e)' width='100%25' height='100%25'/%3E%3Crect fill='url(%23f)' width='100%25' height='100%25'/%3E%3Crect fill='url(%23g)' width='100%25' height='100%25'/%3E%3C/svg%3E");
    background-attachment: fixed;
    background-size: cover;
}

.addbutton {
    display: none;
}

.todobox {
   box-shadow: #ffffff;
}

h1 {
    text-align: center;
    font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
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

p {
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}

ul {
    list-style-type: none; /* Remove bullets */
}

#todostxt {
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
    position: absolute;
}

.completed {
    text-decoration: line-through;
    background-color: #2196F3;
}

li {
    text-align: center;
}

label {
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}

#label1 {
    position: absolute;
    left: 40%;
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}

#radio1 {
    position: absolute;
    left: 40%;
}

#label2 {
    position: absolute;
    left: 50%;
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}

#radio2 {
    position: absolute;
    left: 50%;
}

#label3 {
    position: absolute;
    left: 60%;
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}

#radio3 {
    position: absolute;
    left: 50%;
}

.delete {
    background-color: red;
    height: 35px;
    width: 35px;
    background-color: #eee;
}


/*
.deletion:hover {
    background-color: #2196F3;
}

.deletion:hover > .delete {
    display: inline-block;
    background-color: red;
    position: absolute;
    right: 2%;
    top: 53.5%;
    height: 35px;
    width: 35px;
    background-color: #eee;
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
  left: 18px;
  top: 13px;
  width: 6px;
  height: 12px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
 /* ////////////////////////////////////////// here is for the radio buttons ////////////////////////////////////////// */

/* Create a custom radio button */
.checkmark2 {
  position: absolute;
  top: 0;
  left: 0;
  height: 25px;
  width: 25px;
  background-color: #eee;
  border-radius: 50%;
}

/* On mouse-over, add a grey background color */
.container:hover input ~ .checkmark2 {
  background-color: #ccc;
}

/* When the radio button is checked, add a blue background */
.container input:checked ~ .checkmark2 {
  background-color: #2196F3;
}

/* Create the indicator (the dot/circle - hidden when not checked) */
.checkmark2:after {
  content: "";
  position: absolute;
  display: none;
}

/* Show the indicator (dot/circle) when checked */
.container input:checked ~ .checkmark2:after {
  display: block;
}

/* Style the indicator (dot/circle) */
.container .checkmark2:after {
 	top: 9px;
	left: 9px;
	width: 8px;
	height: 8px;
	border-radius: 50%;
	background: white;
}

/* other stuff..............

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