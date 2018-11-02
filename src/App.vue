<template>
  <div id="app">
    <!--<div id="nav">-->
      <!--<router-link to="/">Home</router-link> |-->
      <!--<router-link to="/about">About</router-link>-->
    <!--</div>-->
    <!--<router-view/>-->
    <input type="text" v-bind:value="text"  v-on:input="text = $event.target.value" @keyup.enter="addTodo">
    <br>
    <label>
      <input type="radio" value="All" v-model="textFiltered">All
    </label>
    <label>
      <input type="radio" value="finished" v-model="textFiltered">Finished
    </label>
    <label>
      <input type="radio" value="unfinished" v-model="textFiltered">Unfinished
    </label>
    <!--<input type="text" v-model="text" @keyup.enter="addTodo">-->
    <ul>
      <Todoitem v-for="item of filteredTodos" :key="item.id" :todoitem="item"  @remove="deleteTodo(item.id)" @update="updateTodo"></Todoitem>
    </ul>

    <pre>{{ $data }}</pre>

  </div>
</template>

<script>
import Todoitem from "./components/Todoitem.vue";
let id = 0;
export default {
  components: {
    Todoitem
  },

  data() {
    return {
      text: "",
      textFiltered: "All",
      todos: [
        { text: "todo item 1", isFinished: true, isEditing: false, id: id++ },
        { text: "todo item 2", isFinished: false, isEditing: true, id: id++ },
        { text: "todo item 3", isFinished: false, isEditing: true, id: id++ }
      ]
    };
  },

  methods: {
    addTodo() {
      if (!this.text) return;
      this.todos.push({ text: this.text, isFinished: false, isEditing: true, id: id++ });
      this.text = "";
    },
    deleteTodo(id) {
      this.todos.splice(this.todos.findIndex(todo => todo.id === id), 1)
    },
    updateTodo(newTodo){
      this.todos.splice(this.todos.findIndex(t => newTodo.id === t.id), 1, newTodo);
    }
  },

  computed: {
    finishedTodos() {
      return this.todos.filter(todo => todo.isFinished);
    },
    unFinishedTodos() {
      return this.todos.filter(todo => !todo.isFinished);
    },
    filteredTodos() {
      if(this.textFiltered === "finished") return this.finishedTodos;
      if(this.textFiltered === "unfinished") return this.unFinishedTodos;
      return this.todos;
    }
  }
};
</script>

<style lang="less">
ul {
  list-style-type: none;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
