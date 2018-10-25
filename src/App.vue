<template>
  <div id="app">
    <!--<div id="nav">-->
      <!--<router-link to="/">Home</router-link> |-->
      <!--<router-link to="/about">About</router-link>-->
    <!--</div>-->
    <!--<router-view/>-->
    <ul>
      <Todoitem v-for="item in todos" v-bind:todoitem="item" @toggle="toggle(item)"></Todoitem>
    </ul>

  </div>
</template>

<script>
    import Todoitem from "./components/Todoitem.vue";
    export default {
        components: {
            Todoitem
        },

        data(){
            return {
                todos: [
                    {text: 'todo item 1', seen: true},
                    {text: 'todo item 2', seen: true},
                    {text: 'todo item 3', seen: false}
                ]
            }
        },

        methods: {
            toggle(todo){
                if(todo.seen){
                    todo.seen = false;
                }else{
                    todo.seen = true;
                }
            }
        }
    }
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
