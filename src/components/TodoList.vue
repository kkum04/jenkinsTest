<template lang="pug">
  .row
    .col-md-6
      .todolist
        h1 Todos
        input.form-control.add-todo(type='text',
                                    placeholder='Add todo'
                                    ref="title"
                                    v-model="title")
        button#btnAddTodo.btn.btn-success(@click='addTodo') 추가
        hr

        ul.list-group
          li.list-group-item(v-for="todo in todoList")
            .row
              .checkbox.col-md-6
                label
                  input(type="checkbox")
                  span {{todo.title}}
              .col-md-6.text-right
                button.btn.btn-default(@click="changeTodo(todo)") 수정
                button.btn.btn-danger(@click="deleteTodo(todo)") 삭제
                button.btn.btn-success(@click="updateToDone(todo)") 완료
</template>

<script>
  import {store} from '../store.js'

  export default {
    name: 'todo-list-component',
    data: function () {
      return {
          title: ''
      }
    },
    methods: {
      addTodo: function () {
        if( this.title === '' ) {
          alert('title');
          this.$refs.title.focus();

          return false;
        }

        store.todoList.push({
          title: this.title,
          isDone: false
        });

        console.dir(store);

        this.title = '';
      },

      deleteTodo: function (todo) {
        if( confirm("삭제?") == false ) {
          return false;
        }

        var index = store.todoList.indexOf(todo);
        if(index == -1) return;

        store.todoList.splice(index, 1);
      },

      updateToDone: function (todo) {
        if( confirm("완료?") == false ) {
          return false;
        }

        todo.isDone = true;
      },

      changeTodo: function (todo) {
        store.selectedTodo = todo;
        router.push('/change')
      }
    },
    computed: {
      todoList: function () {
        return store.todoList.filter(function (todo) {
          return todo.isDone === false;
        });
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  header{
    border-bottom: 1px solid black;
    margin-bottom: 50px;
  }
</style>
