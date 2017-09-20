<template>
  <div class="panel panel-primary todo">

    <div v-if="data.mode">
      <div class="panel-heading">{{data.title}}</div>
      <div class="panel-body">
        <ul class="todo-list">
          <li v-for="(l, index) in data.list" class="todo-list-item">
            <table>
              <tr>
                <td style="width: 20px"><input type="checkbox" v-model="data.list[index].status" :id="l.id" class="pull-left"/></td>
                <td><label :for="l.id"  class="pull-left">{{l.value}}</label></td>
                <td><label class="glyphicon glyphicon-remove pull-right remove" v-on:click="remove(index)"></label></td>
              </tr>
            </table>
          </li>
          <li><input class="todo-input" v-model="newVal" @keyup.enter="addTodo"/></li>
        </ul>
        <button v-on:click="switchMode" class="btn btn-primary btn-sm control-btn pull-left"><label class="glyphicon glyphicon-pencil"></label></button>
        <button class="btn btn-danger btn-sm control-btn pull-right" v-on:click="deleteFunc(index)"><label class="glyphicon glyphicon-trash"></label></button>
      </div>
    </div>

    <div v-else>
      <div class="panel-heading">
        <input type="text" v-model="data.title"/>
      </div>
      <div class="panel-body">
          <ul class="todo-list">
            <li v-for="(l, index) in data.list">
              <input type="text" class="todo-input"  v-model="data.list[index].value"/>
            </li>
          </ul>
          <button v-on:click="switchMode" class="btn btn-success btn-sm pull-right">
            <label class="glyphicon glyphicon-floppy-save"></label> &nbsp;Save
          </button>
      </div>
    </div>

  </div>


</template>

<script>
  export default {
    name: 'todo',
    props:["data", "index", "deleteFunc"],
    data() {
      return {
        newVal: ''
      }
    },
    methods: {
      addTodo: function(){
        if(this.newVal !== "") this.data.list.push({value: this.newVal, status: false, id: Date.now()});
        this.newVal = '';
      },
      switchMode: function(){
        this.data.mode = !this.data.mode;
      },
      remove: function(index){
        console.log("adasd");
        this.data.list.splice(index, 1);
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  label{
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
  }

  .todo{
    float: left;
    text-align: left;
    margin: 10px;
  }

  .todo-list{
    padding-left: 5px;
  }

  .todo-list li{
    list-style: none;
    padding: 5px;
    border-radius: 5px;
  }

  .todo-list-item:hover{
    background-color: lightcyan;
  }

  .todo-list-item:hover .remove{
    background-color: whitesmoke;
    display: block;
  }

  .todo-list-item table{
    width: 100%;
  }

  .todo-input{
    border-style: none;
    border-bottom-style: dashed;
    border-bottom-width: 1px;
    outline: none;
    width: 100%;
    padding: 5px;
    margin-top: 10px;
  }

  input[type='checkbox']{
    vertical-align: middle;
    height: 20px;
    width: 20px;
    margin-right: 10px;
  }

  .remove{
    cursor: pointer;
    display: none;
  }

  .remove:hover{
    color: maroon;
  }





</style>
