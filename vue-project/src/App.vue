<template>
  <body>
    <div class="container">
      <h1>Todos</h1>
      <button @click="toggleAddTodo = !toggleAddTodo">{{!toggleAddTodo ? 'Add todo' : 'Close'}}</button>
      <button @click="toggleAnswer = !toggleAnswer">{{!toggleAnswer ? 'Hide complited' : 'Show all'}}</button>

      <form v-if="toggleAddTodo" @submit.prevent="addTodo">
        <input v-model="newTodo" placeholder="pishi">
        <button>Add todo</button>
      </form>

      <h1 v-if="filtredTodos.length == 0">You have complited all todos</h1>
      <section v-for="todo in filtredTodos" :key="todo.id">
        <label>
          <input type="checkbox" v-model="todo.done">
          <p :class="{ done: todo.done }">{{ todo.name }}</p>
        </label>
        <button @click="deleteTodo(todo)">X</button>
      </section>
      <!-- <TodoItem
          v-for="todo in filtredTodos" 
          :todo="todo"
          :todos="todos"
          :key="todo.id"
          ></TodoItem> -->


    </div>
    <TodoItem>Some text</TodoItem>
  </body>
</template>



<script>
import todoItem from './components/todoItem.vue';
let id = 0;
export default {
  components: {
    todoItem,

},
  data() {
    return {
      toggleAddTodo: false,
      toggleAnswer: false,
      newTodo: '',
      todos: [
        { id: id++, name: 'Alex', done: true },
        { id: id++, name: 'Ivan', done: true },
        { id: id++, name: 'John', done: false },
        { id: id++, name: 'Vitec', done: false }
      ],
    }
  },
  computed: {
    filtredTodos() {
      if (this.toggleAnswer) return this.todos.filter(t => t.done == false)
      return this.todos
    }
  },

  methods: {
    addTodo() {
      this.todos.push({ id: id++, name: this.newTodo, done: false })
      this.newTodo = ''
    },
    deleteTodo(todo) {
      this.todos = this.todos.filter((t) => t !== todo)
    },

  }

}
</script>



<style>
h1 {
  font-size: 3em;
}

p {
  font-size: 1.5em;
}

button {
  padding: 0.3em;
  font-size: 1.5em;
  cursor: pointer;
}

.container {
  box-shadow: 0px 0px 5px 1px;
  margin-top: 20%;
  text-align: center;
  background: rgba(89, 255, 63, 0.2);
}

.container>h1 {
  border-bottom: 3px solid rgba(0, 0, 0, 0.401);
  padding: 0.5em 0;
}

section {
  display: flex;
  padding: 1em;
  border-top: 1px solid rgba(0, 0, 0, 0.5);
  justify-content: space-between;

}

section button {
  width: 2em;
  height: 2em;
  background-color: red;
  color: white;
  border: none;
}

section button:hover {
  transform: scale(1.2);
}

section button {
  transition-property: all;
  transition: all ease .3s;
}

label input[type=checkbox] {
  width: 1.5em;
  height: 1.5em;
}

label p {
  margin: 0 0.5em;
}

label {
  display: flex;
  align-items: center;
}

.container>button {
  background: transparent;
  margin: 1em;
}

form {
  display: flex;
  justify-content: center;
  padding-bottom: 0.5em;
}

form>input {
  padding: 0.5em;
  display: inline-block;

}

.done {
  text-decoration: line-through;
}
</style>