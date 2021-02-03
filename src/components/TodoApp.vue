<template>
    <div>
        <input type="text" class="todo-input" v-model="newTodo" :placeholder="inputPlaceHolder" @keyup.enter="AddToDo">
        <div  v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
            <div class="todo-title-label">
                <input class="item-checkbox" type="checkbox" v-model="todo.completed">
                <div v-if="!todo.editingStatus" @dblclick="canEdit(todo)" :class="{itemChecked : todo.completed}" > {{todo.title}} </div>
                <input v-else type="text" class="editInput" v-model="todo.title" @blur="editingCompleted(todo)" @keyup.enter="editingCompleted(todo)" @keyup.esc="cancelEdit(todo)" v-focus>
            </div>
            <div class="remove-item" @click="removeTodo(index)">&times;</div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'todo-list',
  data() {
      return {
          inputPlaceHolder: "Type What You Hope Todo Here",
          newTodo: "",
          todosIdInc: 3,
          beforeEditCache: '',
          todos: [
              {
                  'id': 1,
                  'title': 'Playing football',
                  'editingStatus': false,
                  'completed' : false
              },
              {
                  'id': 2,
                  'title': 'Studing English',
                  'editingStatus': false,
                  'completed' : false
              },

          ]
      }
  },
methods: {
    AddToDo() {
        if(this.newTodo.trim().length > 0){
        this.todos.push({
            'id': this.todosIdInc,
            'title': this.newTodo,
            'editingStatus': false,
            'completed' : false

        })
        this.newTodo=""
        this.todosIdInc++
        }else {
            alert("You Should Write Something")
        }
    },
    removeTodo(index) {
        this.todos.splice(index, 1);
    },
    canEdit(todo) {
        this.beforeEditCache = todo.title
        todo.editingStatus = true;
    },
    editingCompleted(todo){
        if(todo.title.trim().length == 0){
            todo.title = this.beforeEditCache
        }else{
            todo.editingStatus = false;
        }
    },
    cancelEdit(todo) {
        todo.title = this.beforeEditCache
        todo.editingStatus = false;
    }
},
directives: {
  focus: {
    inserted: function (el) {
      el.focus()
    }
  }
},
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >
.todo-input {
    width:100%;
    margin-bottom: 10px;
    padding:10px 3px;
    border-color: #41b883 !important;
    border-radius: 10px
}
.todo-input:focus {
    outline: none
}
.editInput {
    width: 75%;
    border-color: #41b883;
    border-radius: 5px;
    padding: 8px;
}
.todo-item {
    text-align: left;
    margin-bottom: 10px;
    display: flex;
    justify-content: space-between;
}
.todo-title-label {
    display: flex;
}
.item-checkbox{
    margin: 5px 18px 0 0 ;
}
.itemChecked {
    text-decoration: line-through;
}
.remove-item {
    cursor: pointer;
    color: grey
}
.remove-item:hover {
    color: black
}
</style>
