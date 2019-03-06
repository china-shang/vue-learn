<template>
  <div>
    <BaseInputText v-model="todoAuthor" placeholder="New todo">
      <label>Your Name:</label>
    </BaseInputText>
    <BaseInputText
      v-model="newTodoText"
      placeholder="Name"
      @keydown.enter="addTodo"
    >
      <label>Your Todo:</label>
    </BaseInputText>

    <button @click="addTodo">Add</button>

    <ul v-if="todos.length">
      <TodoListItem
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        @remove="removeTodo"
      >
        <template slot="first">
          <b> this used for {{ todo.author ? todo.author : "Anonymous" }} </b>
        </template>
        <template v-slot:last>
          <b> this used for {{ todo.author ? todo.author : "Anonymous" }} </b>
        </template>
      </TodoListItem>
    </ul>
    <p v-else>Nothing left in the list. Add a new todo in the input above.</p>
  </div>
</template>

<script>
import BaseInputText from "./BaseInputText.vue";
import TodoListItem from "./TodoListItem.vue";

let nextTodoId = 1;

export default {
  components: {
    BaseInputText,
    TodoListItem
  },
  data() {
    return {
      newTodoText: "",
      todoAuthor: "",
      todos: [
        {
          id: nextTodoId++,
          text: "Learn Vue",
          author: "Mark"
        },
        {
          id: nextTodoId++,
          text: "Learn about single-file components",
          author: "Honi"
        },
        {
          id: nextTodoId++,
          text: "Fall in love",
          author: "John"
        }
      ]
    };
  },
  methods: {
    addTodo() {
      const trimmedText = this.newTodoText.trim();
      const trimmedAuthor = this.todoAuthor;
      const a = this.$root;
      alert(a);

      if (trimmedText) {
        this.todos.push({
          id: nextTodoId++,
          text: trimmedText,
          author: trimmedAuthor
        });
        this.newTodoText = "";
      }
    },
    removeTodo(idToRemove) {
      this.todos = this.todos.filter(todo => {
        return todo.id !== idToRemove;
      });
    }
  }
};
</script>
