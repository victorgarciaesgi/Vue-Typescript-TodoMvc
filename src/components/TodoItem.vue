<template>
  <li class="todo" :class="{ completed: todo.completed, editing: todo == editedTodo }">
    <div class="view">
      <input class="toggle" type="checkbox" v-model="todo.completed">
      <label @dblclick="editTodo(todo)">{{ todo.title }}</label>
      <button class="destroy" @click="removeTodo(todo)"></button>
    </div>
    <input class="edit" type="text"
      v-model="todo.title"
      v-todo-focus="todo == editedTodo"
      @blur="doneEdit(todo)"
      @keyup.enter="doneEdit(todo)"
      @keyup.esc="cancelEdit(todo)">
  </li>
</template>

<script lang="ts">
import Vue from "vue";
import Component from "vue-class-component";
import { Prop } from "vue-property-decorator";
import { State, Getter, Mutation, Action, namespace } from "vuex-class";


const TodoGetter = namespace("TodoModule", Getter);
const TodoMutation = namespace("TodoModule", Mutation);
const TodoAction = namespace("TodoModule", Action);

@Component({
  components: {},
  directives: {
    "todo-focus": function(el, binding) {
      if (binding.value) {
        el.focus();
      }
    }
  }
})
export default class TodoItem extends Vue {
  @Prop() todo;

@TodoMutation removeTodo;
  @TodoAction editTodoAction;

  public beforeEdit = "";
  public editedTodo = null;

  editTodo(todo) {
    this.beforeEdit = todo.title;
    this.editedTodo = todo;
  }

  doneEdit(todo) {
    if (!this.editedTodo) {
      return;
    }
    this.editedTodo = null;
    this.editTodoAction(todo);
  }

  cancelEdit(todo) {
    this.todo.title = this.beforeEdit;
  }
}
</script> 