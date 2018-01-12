<template>
  <div id='app'>
    <section class="todoapp">
      <Header/>
      <TodoList />
      <Footer/>
    </section>
    <footer class="info">
      <p>Double-click to edit a todo</p>
      <p>Written by <a href="https://github.com/victorgarciaesgi">Victor Garcia</a></p>
      <p>Part of <a href="http://todomvc.com">TodoMVC</a></p>
    </footer>
  </div>
</template>


<script lang="ts">
import Vue from "vue";
import Component from "vue-class-component";

import { store } from "@store";
import { Header, TodoList, Footer } from "@components";
import {State,Getter, Mutation, Action, namespace} from 'vuex-class';

const TodoAction = namespace('TodoModule', Action);

@Component({
  components: {
    Header, TodoList, Footer
  },
  store
})
export default class App extends Vue {

  @TodoAction changeVisibility;

  mounted() {
    window.addEventListener('hashchange', this.onHashChange);
    this.onHashChange();
  }

  onHashChange() {
    let visibility = window.location.hash.replace(/#\/?/, '')
    this.changeVisibility(visibility);
  }
}
</script>


<style lang="css">


html,
body {
	margin: 0;
	padding: 0;
}

button {
	margin: 0;
	padding: 0;
	border: 0;
	background: none;
	font-size: 100%;
	vertical-align: baseline;
	font-family: inherit;
	font-weight: inherit;
	color: inherit;
	-webkit-appearance: none;
	appearance: none;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale; 
}

body {
	font: 14px 'Helvetica Neue', Helvetica, Arial, sans-serif;
	line-height: 1.4em;
	background: #f5f5f5;
	color: #4d4d4d;
	min-width: 230px;
	max-width: 550px;
	margin: 0 auto;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	font-weight: 300;
}

:focus {
	outline: 0;
}

.hidden {
	display: none;
}

.todoapp {
	background: #fff;
	margin: 130px 0 40px 0;
	position: relative;
	box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2),
	            0 25px 50px 0 rgba(0, 0, 0, 0.1);
}

.todoapp input::-webkit-input-placeholder {
	font-style: italic;
	font-weight: 300;
	color: #e6e6e6;
}

.todoapp input::-moz-placeholder {
	font-style: italic;
	font-weight: 300;
	color: #e6e6e6;
}

.todoapp input::input-placeholder {
	font-style: italic;
	font-weight: 300;
	color: #e6e6e6;
}

.todoapp h1 {
	position: absolute;
	top: -155px;
	width: 100%;
	font-size: 100px;
	font-weight: 100;
	text-align: center;
	color: rgba(175, 47, 47, 0.15);
	-webkit-text-rendering: optimizeLegibility;
	-moz-text-rendering: optimizeLegibility;
	text-rendering: optimizeLegibility;
}


.info {
	margin: 65px auto 0;
	color: #bfbfbf;
	font-size: 10px;
	text-shadow: 0 1px 0 rgba(255, 255, 255, 0.5);
	text-align: center;
}

.info p {
	line-height: 1;
}

.info a {
	color: inherit;
	text-decoration: none;
	font-weight: 400;
}

.info a:hover {
	text-decoration: underline;
}


@media (max-width: 430px) {
	.footer {
		height: 50px;
	}

	.filters {
		bottom: 10px;
	}
}

</style>

