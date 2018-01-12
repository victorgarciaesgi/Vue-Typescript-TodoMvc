<template>
   <footer class="footer" v-show="TodoState.todos.length" v-cloak>
      <span class="todo-count">
        <strong>{{ remaining }}</strong> {{ remaining | pluralize }} left
      </span>
      <ul class="filters">
        <li><a href="#/all" :class="{ selected: TodoState.visibility == 'all' }">All</a></li>
        <li><a href="#/active" :class="{ selected: TodoState.visibility == 'active' }">Active</a></li>
        <li><a href="#/completed" :class="{ selected: TodoState.visibility == 'completed' }">Completed</a></li>
      </ul>
      <button class="clear-completed" @click="removeCompleted" v-show="TodoState.todos.length > remaining">
        Clear completed
      </button>
    </footer>
</template>


<script lang="ts">
import Vue from "vue";
import Component from "vue-class-component";
import { State, Getter, Mutation, namespace } from "vuex-class";

const TodoGetter = namespace("TodoModule", Getter);
const TodoMutation = namespace("TodoModule", Mutation);

@Component({
  filters: {
    pluralize(n) {
      return n === 1 ? "item" : "items";
    }
  }
})
export default class Footer extends Vue {
  @State("TodoModule") TodoState;
  @TodoGetter remaining;
  @TodoMutation removeCompleted;
}
</script> 


<style>
.footer {
	color: #777;
	padding: 10px 15px;
	height: 20px;
	text-align: center;
	border-top: 1px solid #e6e6e6;
}

.footer:before {
	content: '';
	position: absolute;
	right: 0;
	bottom: 0;
	left: 0;
	height: 50px;
	overflow: hidden;
	box-shadow: 0 1px 1px rgba(0, 0, 0, 0.2),
	            0 8px 0 -3px #f6f6f6,
	            0 9px 1px -3px rgba(0, 0, 0, 0.2),
	            0 16px 0 -6px #f6f6f6,
	            0 17px 2px -6px rgba(0, 0, 0, 0.2);
}

.todo-count {
	float: left;
	text-align: left;
}

.todo-count strong {
	font-weight: 300;
}

.filters {
	margin: 0;
	padding: 0;
	list-style: none;
	position: absolute;
	right: 0;
	left: 0;
}

.filters li {
	display: inline;
}

.filters li a {
	color: inherit;
	margin: 3px;
	padding: 3px 7px;
	text-decoration: none;
	border: 1px solid transparent;
	border-radius: 3px;
}

.filters li a:hover {
	border-color: rgba(175, 47, 47, 0.1);
}

.filters li a.selected {
	border-color: rgba(175, 47, 47, 0.2);
}

.clear-completed,
html .clear-completed:active {
	float: right;
	position: relative;
	line-height: 20px;
	text-decoration: none;
	cursor: pointer;
}

.clear-completed:hover {
	text-decoration: underline;
}
</style>
