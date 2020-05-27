<template>
  <div>
    <md-card>
      <md-card-header class="title">
        <div class="md-title">
          <img class="berry-title" src="./assets/smallberry.png">Memberberry<img class="berry-title" src="./assets/smallberry.png">
        </div>
        <div class="md-subhead">Member all the things you'd forget</div>
      </md-card-header>
      <md-field>
        <md-input
          class="user-input"
          v-model="currentTodo" 
          @keydown.enter="addTodo()" 
          placeholder="Enter something to member">
        </md-input>
      </md-field>
      <ul class="todos">
        <div class="todo-items-container">
        <li 
          class="todo-item"
          v-for="todo in todos"
          :key="todo.id"
          >
          <div class="checkbox-container">
          <input 
            class="completed" 
            type="checkbox" 
            >
          </input>
          </div>
          <div class="span-container">
          <span 
            class="editing"
            v-if="todo.editing === false"
            :class="{editing: todo === editedTodo}"
            @dblclick="editTodo(todo)"
            > {{ todo.label }}
          </span>
          </div>
          <md-field 
            class="editing"
            v-if="todo.editing"
            >
            <md-input
              class="edit-input"
              type="text"
              v-model="todo.label"
              @keyup.enter="finishEdit(todo)"
              @keyup.esc="finishEdit(todo)"
              @focusout="finishEdit(todo)"
              placeholder="Edit task"
              >
            </md-input>
          </md-field>
          <div class="list-buttons">
          <md-button
            class="md-raised main-button"
            v-if="todo.editing === false" 
            @click="editTodo(todo)"
            >Re-member
          </md-button>
           <md-button
            class="md-raised main-button"
            v-if="todo.editing === false"
            @click="removeTodo(todo)"
            >Forget
          </md-button>
          </div>
          <div class="edit-buttons">
          <md-button
            class="md-raised main-button"
            v-if="todo.editing === true"
            @click="finishEdit(todo)"
            >Oh now I member
          </md-button>
          </div>
        </li>
        </div>
      </ul>
    </md-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: '',
      editedTodo: ''
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length,
        label: this.currentTodo,
        completed: false,
        editing: false
      });
      this.currentTodo = '';
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    editTodo(todo, toggle) {
      const index = this.todos.indexOf(todo);
      this.todos[index].editing = !this.todos[index].editing;
    },
    finishEdit(todo) {
      todo.editing= false;
    }
  }
};
</script>

<style>
body{
  background-image: url("./assets/background.png")
}

.md-card {
  background: tan;
  max-width: 40rem;
  margin-left: auto;
  margin-right: auto;
}

.title {
  text-align: center;
  color: purple;
}

.user-input {
  text-align: center;
  text-decoration: purple underline;
}

.edit-input {
  display: flex;
  text-align: center;
  justify-content: space-around;
  border: 2px solid green !important;
}

.list-buttons {
  text-align: center;
}

.edit-buttons {
  display: flex;
  flex-direction: ;
  margin: 1rem;
}

.todo-items-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
  margin: 1rem;
}

.todo-item {
  text-align: center;
}

span {
  border: 2px solid purple;
  padding: .5rem;
  font-size: 18px;
}

.span-container {
  margin: .5rem;
}

.checkbox-container {
  text-align: center;
  margin-bottom: 1rem;
}

ul {
  list-style-type: none;
  padding: 0;
}

.md-raised,
.main-button,
.md-ripple {
  background: purple;
  color: white;
}
</style>
