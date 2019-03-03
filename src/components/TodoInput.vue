<template>
  <div>
    <h2>新規タスクの追加</h2>
    <input type="text" :value="value" @input="updateText">
    <button @click="addTodo">追加</button>
  </div>
</template>

<script>
export default {
  props: ["value", "addTodo"],
  methods: {
    updateText(e) {
      this.$emit("input", e.target.value);
    }
  }
};
</script>