<template>
  <div id="app">
    <!--<div id="nav">-->
      <!--<router-link to="/">Home</router-link> |-->
      <!--<router-link to="/about">About</router-link>-->
    <!--</div>-->
    <!--<router-view/>-->
    <input type="text" v-bind:value="text"  v-on:input="text = $event.target.value" @keyup.enter="addTodo">
    <!--<input type="text" v-model="text" @keyup.enter="addTodo">-->
    <ul>
      <Todoitem v-for="(item, i) of todos" :key="item.id" :todoitem="item" @toggle="toggle" @remove="deleteTodo(todos, item.id)"></Todoitem>
      <Todoitem v-for="(item, i) in todos2" :key="item.id" v-bind:todoitem="item" @toggle="toggle" @remove="deleteTodo(todos2, item.id)"></Todoitem>
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
      text: "Type your text",
      todos: [
        { text: "todo item 1", seen: true, isEditing: true, id: id++ },
        { text: "todo item 2", seen: true, isEditing: true, id: id++ },
        { text: "todo item 3", seen: false, isEditing: false, id: id++ }
      ],
      todos2: [
        { text: "todo item 1", seen: true, isEditing: true, id: id++ },
        { text: "todo item 2", seen: true, isEditing: true, id: id++ },
        { text: "todo item 3", seen: false, isEditing: false, id: id++ }
      ]
    };
  },

  methods: {
    addTodo() {
      if (!this.text) return;
      this.todos.push({ text: this.text, seen: true, isEditing: true, id: id++ });
      this.text = "";
    },
    deleteTodo(array, id) {
      console.log("delete todo item ", id);
      array.splice(array.findIndex(todo => todo.id === id), 1)
    }
  },

  computed: {
    toggle() {
      return this.todos.filter(todo => (todo.seen ? !todo.seen : todo.seen));
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
