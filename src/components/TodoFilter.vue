<template>
  <ul class="filter">
    <li>
      <input
        type="radio"
        id="todo_state_filter_1"
        name="todo_state_filter"
        value="all"
        @click="filterTodoByState"
        :checked="filter_mode == 'all'"
      >
      <label for="todo_state_filter_1">すべて</label>
    </li>
    <li>
      <input
        type="radio"
        id="todo_state_filter_2"
        name="todo_state_filter"
        value="working"
        @click="filterTodoByState"
        :checked="filter_mode == 'working'"
      >
      <label for="todo_state_filter_2">作業中</label>
    </li>
    <li>
      <input
        type="radio"
        id="todo_state_filter_3"
        name="todo_state_filter"
        value="done"
        @click="filterTodoByState"
        :checked="filter_mode == 'done'"
      >
      <label for="todo_state_filter_3">完了</label>
    </li>
  </ul>
</template>

<script>
export default {
  props: ["filterTodoByState", "filter_mode"]
};
</script>