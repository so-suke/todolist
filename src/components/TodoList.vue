<template>
  <div>
    <TodoFilter :filterTodoByState="filterTodoByState" :filter_mode="filter_mode"></TodoFilter>
    <table class="table">
      <tr>
        <th>ID</th>
        <th>コメント</th>
        <th>状態</th>
      </tr>
      <TodoItem
        v-for="(todo, idx) in filteredTodos"
        v-bind:key="todo.id"
        v-bind:idx="idx"
        v-bind:todo="todo"
        :toggleTodoState="toggleTodoState"
        :deleteTodo="deleteTodo"
      ></TodoItem>
    </table>
    <TodoInput v-model="new_comment" :addTodo="addTodo"></TodoInput>
  </div>
</template>

<script>
import TodoFilter from "./TodoFilter.vue";
import TodoItem from "./TodoItem.vue";
import TodoInput from "./TodoInput.vue";

import { TODO_STATE } from "../static/enumerations.js";
import { filters } from "../static/functions.js";

export default {
  components: {
    TodoFilter,
    TodoItem,
    TodoInput
  },
  data() {
    return {
      todos: [],
      new_comment: "", // 新規todoコメント入力用inputの値
      filter_mode: "all" // todoリストをフィルタリングするモード。(初期モードは、全て)
    };
  },
  methods: {
    // 新規todo追加
    addTodo: function() {
      if (this.new_comment === "") {
        return;
      }
      this.todos.push({
        comment: this.new_comment,
        state: TODO_STATE.WORKING
      });
      this.new_comment = "";
    },
    // 各todoの状態を切り替えます(作業中と完了で切り替えます。)
    toggleTodoState: function(todo) {
      if (todo.state === TODO_STATE.WORKING) {
        todo.state = TODO_STATE.DONE;
      } else if (todo.state === TODO_STATE.DONE) {
        todo.state = TODO_STATE.WORKING;
      }
    },
    // 各todoを削除。
    deleteTodo: function(todo) {
      this.todos.splice(this.todos.indexOf(todo), 1);
    },
    // todoリストのフィルタリング用モードを変更します。
    filterTodoByState: function(event) {
      this.filter_mode = event.currentTarget.value;
    }
  },
  computed: {
    // 設定されているフィルターモードを元にtodoリストをフィルタリングします。
    filteredTodos: function() {
      return filters[this.filter_mode](this.todos);
    }
  }
};
</script>

<style>
ul,
li {
  list-style: none;
  margin: 0;
  padding: 0;
}

.filter {
  display: flex;
  margin-bottom: 20px;
}
</style>
