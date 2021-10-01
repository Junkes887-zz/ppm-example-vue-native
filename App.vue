<template>
  <view class="container">
    <Statusbar color="#5B11BF" />
    <Header title="Tarefas"/>

    <view class="inputContainer">
      <text-input class="input" v-model="newTodoText" placeholder="Tarefa..."/>
      <touchable-opacity class="add-btn" :on-press="newTodo">
        <text class="btn-text">+</text>
      </touchable-opacity>
    </view>

    <view class="todo" v-for="todo in todos" :key="todo.id">
      <touchable-opacity :on-press="() => toggleDone(todo.id)">
        <text class="todo-text done" v-if="todo.done">{{ todo.title }}</text>
        <text class="todo-text" v-else>{{ todo.title }}</text>
      </touchable-opacity>
      <touchable-opacity class="remove-btn" :on-press="() => removeTodo(todo.id)">
        <text class="remove-btn-text">-</text>
      </touchable-opacity>
    </view>
  </view>
</template>

<script>
import Statusbar from './components/Statusbar'
import Header from './components/Header'

export default {
  data() {
    return {
      newTodoText: '',
      todos: [
        {
          id: 0,
          title: 'Tarefa 1',
          done: false
        },
        {
          id: 1,
          title: 'Tarefa 2',
          done: false
        }
      ]
    }
  },

  components: {
    Statusbar,
    Header
  },

  methods: {
    newTodo() {
      this.todos.push({
        id: this.todos.length + 1,
        title: this.newTodoText,
        done: false
      });
      this.newTodoText = '';
    },
    toggleDone (id) {
      this.todos = this.todos.map(todo => {
        if (todo.id == id) todo.done = !todo.done;
        return todo;
      })
    },
    removeTodo (id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    }
  }
}
</script>

<style>
.container {
  background-color: white;
  flex: 1;
}
.inputContainer {
  flex-direction: row;
  justify-content: center;
  align-items: stretch;
}
.input {
  flex: 1;
  height: 35px;
  background-color: #F3F3F3;
  font-size: 18px;
  color: #888888;
  padding-left: 5px;
}
.add-btn {
  width: 100px;
  height: 35px;
  background-color: #097a06;
  justify-content: center;
  align-items: center;

}
.btn-text {
  font-size: 18px;
  font-weight: 700;
  color: #F3F3F3;
}
.todo {
  flex-direction: row;
  justify-content: space-between;
  padding: 15px;
}
.todo-text {
  font-size: 18px;
  color: #202020;
}
.done {
  color: #0b913e;
}
.remove-btn {
  width: 60px;
  height: 35px;
  background-color: rgb(201, 12, 12);
  justify-content: center;
  align-items: center;
  border-radius: 20px;
  padding-bottom: 5px;
}

.remove-btn-text {
  font-size: 18px;
  color: #F3F3F3;
}
</style>