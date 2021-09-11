<template>
  <div>
    <div class="container">
      <input type="text" class="todo-input" placeholder="Task name" v-model="newTodo" @keyup.enter="addTodo">
      <button type="button" @click="addTodo">Add task</button> 
    </div>
    <input type="text" class="filter" v-model="search" placeholder="Filter">
    <div v-for="(todo,index) in filteredItems" :key="todo.id" class="todo-item" :class="{ completed : todo.completed }">
      <div class="todo-item-left">
        <input type="checkbox" v-model="todo.completed">
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
      idToDo: 4,
      tempTitle: '',
      search: '',
      todos:[
        {
          'id': 1,
          'title': 'Buy bread',
          'completed': true,
          'editing': false,
        },
        {
          'id': 2,
          'title': 'Be responsible',
          'completed': false,
          'editing': false,
        },
        {
          'id': 3,
          'title': "Try not to destroy your window's motor",
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
  computed: {
    filteredItems() {
      if(this.search ==''){
        return this.todos
      }
      else{
        return this.todos.filter(todo => todo.title.toLowerCase().includes(this.search.toLowerCase()))
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

.container {
  margin-bottom: 10px;
}

.todo-input { 
  width: 80%; 
  padding: 10px;
}

.filter { 
  width: 100%;
  margin-bottom: 10px;
  padding: 10px; 
}

.todo-item {
  display: flex;
  justify-content: space-between;
  padding: 2px 5px;
  border-bottom: 1px solid #e2e2e2;
  /* border-radius: 10px; */
  transition: 0.8s;
}

.remove-item, .edit-item {
  cursor: pointer;
  align-self: center;
  margin: 0 10px;
  font-size: 25px;
}

button {
   background: green;
   padding: 10px;
   color: white;
   margin-left: 15px;
   transition: 0.5s;
}

button:hover {
  background: #015f01;
}

.todo-item-left {
  display:flex;
  align-items: center;
}

.todo-item-label, .todo-item-edit { 
  margin-left: 5px;
  padding: 10px;
  font-size:18px;
  text-decoration: line-through rgba(255,255,255,0);
}

.interactive-elements { 
  display:flex;
  flex-direction: row;
}

.completed { 
  background: #c7c7c7;
  transition: 0.8s;
}

.completed .todo-item-label {
  transition: 0.8s;
  text-decoration: line-through #2c3e50;
}


</style>
