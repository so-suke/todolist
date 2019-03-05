<template>
  <tr>
    <td>{{ idx }}</td>
    <td>{{ todo.comment }}</td>
    <td>
      <button @click="toggleTodoState(todo)">{{ todo.state }}</button>
      <button @click="deleteTodo(todo)">削除</button>
    </td>
  </tr>
</template>

<script>
export default {
  props: ["idx", "todo", "toggleTodoState", "deleteTodo"]
};
</script>