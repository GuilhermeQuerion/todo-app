<template>
  <h1>Todo App</h1>
  <div v-if="!editMode">
    <ButtonVue @click="newTodo">Novo</ButtonVue>
    <todo-list :todos="todos" @deleta="deleta" @edit="edit"></todo-list>
  </div>
  <todo-item
    v-if="editMode"
    @cancel="cancel"
    @saveTodo="saveTodo"
    :todo="todo"
  ></todo-item>
</template>

<script>
import TodoItem from "./components/TodoItem.vue";
import TodoList from "./components/TodoList.vue";

export default {
  components: {
    TodoList,
    TodoItem,
  },
  data() {
    return {
      editMode: false,
      todos: [],
      todo: null,
      nextid: 1,
    };
  },
  methods: {
    newTodo() {
      this.todo = null;
      this.editMode = true;
    },
    cancel() {
      this.editMode = false;
    },
    saveTodo(todo) {
      if (todo.id) {
        const index = this.todos.findIndex((item) => item.id === todo.id)
        this.todos[index] = todo;
      } else {
        todo = { id: this.nextid, ...todo };
        this.todos.push(todo);
        this.nextid++;
        localStorage.setItem("nextId", this.nextid);
      }
      localStorage.setItem("todos", JSON.stringify(this.todos));
      this.editMode = false;
    },
    deleta(index) {
      this.todos.splice(index, 1);
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
    edit(index) {
      this.todo = this.todos[index];
      this.editMode = true;
    },
  },
  created() {
    const todos = localStorage.getItem("todos");
    if (todos) {
      this.todos = JSON.parse(todos);
    }
    const nextid = localStorage.getItem("nextId");
    if (nextid) {
      this.nextid = parseInt(nextid);
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
}
</style>
