<template>
  <div>
    <div class="container">
      <input type="text" class="todo-input" placeholder="Item name" v-model="newTodo" @keyup.enter="addTodo">
      <button type="button" v-on:click="addTodo">Add task</button> 
    </div>
    <div v-for="(todo,index) in todos" :key="todo.id" class="todo-item">
      <div class="todo-item-left">
        <div v-if="!todo.editing" @dblclick="editTodo(todo)" class="todo-item-label">{{todo.title}}</div>
        <input v-else class="todo-item-edit" type="text" v-model="todo.title" @blur="doneEdit(todo)" @keyup.enter="doneEdit(todo)" @keyup.esc="cancelEdit(todo)" v-focus>
      </div>
      <div class="interactive-elements">
        <div class="edit-item" @click="editTodo(todo)">
          &#x270E;
        </div>
        <div class="remove-item" @click="removeToDo(index)">
          &times;
        </div>
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
      tempTitle: '',
      todos:[
        {
          'id': 1,
          'title': 'Buy bread',
          'completed': false,
          'editing': false,
        },
        {
          'id': 2,
          'title': 'Be responsible',
          'completed': false,
          'editing': false,
        }
      ]
    }
  },
  directives: {
    focus: {
      // directive definition
      inserted: function (el) {
        el.focus()
      }
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
        editing: false,
      })

      this.newTodo = ''
      this.this.idToDo++
    },
    editTodo(todo){
      this.tempTitle = todo.title
      todo.editing = true
    },
    removeToDo(index){
      this.todos.splice(index, 1)
    },
    cancelEdit(todo){
      todo.title = this.tempTitle
      todo.editing = false
    },
    doneEdit(todo){
      if(todo.title.trim()==0){
        todo.title = this.tempTitle
      }
      todo.editing = false
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

.todo-item {
  margin: 5px 0;
  display: flex;
  justify-content: space-between;
  padding: 0px 5px;
}

.remove-item, .edit-item {
  cursor: pointer;
  align-self: center;
  margin-left: 15px;
  font-size: 25px;
}

button {
   background: green;
   padding: 10px;
   color: white;
   margin-left: 15px;
}

.todo-item-left {
  display:flex;
  align-items: center;
}

.todo-item-label, .todo-item-edit { 
  margin-left: 5px;
  padding: 10px;
  font-size:18px;
}

.interactive-elements { 
  display:flex;
  flex-direction: row;
}



</style>
