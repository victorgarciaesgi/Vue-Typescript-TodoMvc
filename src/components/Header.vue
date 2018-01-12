<template>
   <header class="header">
      <h1>todos</h1>
      <input class="new-todo"
        autofocus autocomplete="off"
        placeholder="What needs to be done?"
        v-model="newTodo"
        @keyup.enter="add">
    </header>
</template>


<script lang="ts">
import Vue from "vue";
import Component from "vue-class-component";
import { State, Mutation, Action, namespace } from "vuex-class";
import { ITodosState } from "@types";

const TodoAction = namespace("TodoModule", Action);

@Component({})
export default class Header extends Vue {
  @TodoAction addTodoAction;
  public newTodo: string = "";

  add() {
    if (this.newTodo.length) {
      this.addTodoAction(this.newTodo.trim());
      this.newTodo = "";
    }
  }
}
</script> 

<style>

.new-todo,
.edit {
	position: relative;
	margin: 0;
	width: 100%;
	font-size: 24px;
	font-family: inherit;
	font-weight: inherit;
	line-height: 1.4em;
	border: 0;
	color: inherit;
	padding: 6px;
	border: 1px solid #999;
	box-shadow: inset 0 -1px 5px 0 rgba(0, 0, 0, 0.2);
	box-sizing: border-box;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
}

.new-todo {
	padding: 16px 16px 16px 60px;
	border: none;
	background: rgba(0, 0, 0, 0.003);
	box-shadow: inset 0 -2px 1px rgba(0,0,0,0.03);
}
</style>
