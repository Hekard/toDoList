<template>
  <div>
    <div class="container">
      <input type="text" class="todo-input" placeholder="Item name" v-model="newTodo" @keyup.enter="addTodo">
      <button type="button" v-on:click="addTodo">Add task</button> 
    </div>
    <div v-for="(todo,index) in todos" :key="todo.id" class="toDoItem">
      <div class="toDo">
        <div>{{todo.title}}</div>
        <input type="text" v-model="todo.title">
      </div>
      <div class="remove-item" @click="removeToDo(index)">
        &times;
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      newTodo: '',
      idToDo: 3,
      todos:[
        {
          'id': 1,
          'title': 'Buy bread',
          'completed': false,
        },
        {
          'id': 2,
          'title': 'Be responsible',
          'completed': false,
        }
      ]
    }
  },
  methods: {
    addTodo(){
      if(this.newTodo.trim()==0){
        return
      }

      this.todos.push({
        id: this.idToDo,
        title: this.newTodo,
        completed: false,
      })

      this.newTodo = ''
      this.this.idToDo++
    },
    removeToDo(index){
      this.todos.splice(index, 1)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.todo-input { 
  width: 80%; 
  padding: 10px;
}

.toDoItem {
  margin: 5px 0;
  display: flex;
  justify-content: space-between;
  padding: 0px 5px;
}

.remove-item {
  cursor: pointer;
}

button {
   background: green;
   padding: 10px;
   color: white;
   margin-left: 15px;
}


h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
