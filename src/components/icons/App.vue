  <template>
    <div id="app">
  
      <h1>Liste des Produits</h1>
      <input
        v-model="newTodoText"
        @keyup.enter="addTodo"
        placeholder="Ajouter une nouvelle tâche"
      />
      <button @click="addTodo">Ajouter</button>
      <div class="todo-list">
        <TodoItem
          v-for="todo in todos"
          :key="todo.id"
          :todo="todo"
          @delete-todo="deleteTodo"
          @update-todo="updateTodo"
        />
      </div> 
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import TodoItem from './components/todoItem.vue';
  
  const newTodoText = ref('');
  const todos = ref([
    { id: 1, text: 'Samsung', completed: false },
    { id: 2, text: 'Iphone', completed: false },
    { id: 2, text: 'Huawei', completed: false },
  ]);
  
  const addTodo = () => {
    if (newTodoText.value.trim() === '') return;
    todos.value.push({
      id: Date.now(),
      text: newTodoText.value,
      completed: false,
    });
    newTodoText.value = '';
  };
  
  const deleteTodo = (id) => {
    todos.value = todos.value.filter(todo => todo.id !== id);
  };
  
  const updateTodo = (updatedTodo) => {
    const index = todos.value.findIndex(todo => todo.id === updatedTodo.id);
    if (index !== -1) {
      todos.value[index] = updatedTodo;
    }
  };
  </script>
  
  <style scoped>
  
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color : green;
    margin-top: 60px;
  }
  .todo-list {
    margin-top: 20px;
    color: brown;
  }
  
  input {
    padding: 10px;
    font-size: 16px;
    border: 1px solid green;
    border-radius: 30px;
  }
  
  button {
    padding: 10px;
    font-size: 20px;
    margin-left: 10px;
    border: 1px solid green;
    border-radius: 30px;
  
  }
  </style>
  
  
  
  
  
  
  
  