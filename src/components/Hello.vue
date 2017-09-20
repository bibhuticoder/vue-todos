<template>
  <div>
    <nav class="navbar navbar-inverse">
      <div class="container-fluid">
        <div class="navbar-header">
          <a class="navbar-brand" href="#">
            Vue-Todos
          </a>
        </div>
        <button  class="pull-right btn btn-success" v-on:click="addTodo">
          <span class="glyphicon glyphicon-list-alt"></span>
          &nbsp;&nbsp; New Todo
        </button>
      </div>
    </nav>

    <div class="container">
      <div v-for="(todo,i) in todos">
        <todo :index="i" :data="todos[i]" :deleteFunc="removeTodo"></todo>
      </div>
    </div>



  </div>


</template>

<script>
import Todo from "./Todo.vue";

export default {
  components: {Todo},
  name: 'hello',
  data () {
    return {
      todos: [
        {
          id: Date.now(),
          title: 'Todo 1',
          mode: true,
          list: [
            {value: 'Do Something', status: false, id: 234}
          ]
        }
      ]
    }
  },

  methods: {
    addTodo(){
      this.todos.push({
        id: Date.now(),
        title: 'New Todo ' + this.todos.length,
        mode: true,
        list: []
      })
    },
    removeTodo(index){
      this.todos.splice(index, 1);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .navbar{
    border-radius: 0px !important;
  }
</style>
