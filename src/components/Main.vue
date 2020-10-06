<template>
  <div>
    <h1>To Do リスト</h1>
      <form>
      <input type="radio" name="status" value="all" checked />全て
      <input type="radio" name="status" value="middle" />作業中
      <input type="radio" name="status" value="done" />完了
    </form>
    <table>
      <tr>
        <th>ID</th>
        <th>コメント</th>
        <th>状態</th>
      </tr>
      <tr v-for="(todo, index) in todos" :key="todo">
        <td>{{index}}</td>
        <td>{{todo.text}}</td>
        <td><button>{{todo.done}}</button></td>
        <td><button @click="deleteTask(index)">削除</button></td>
      </tr>
    </table>
    <h2>新規タスクの追加</h2>
    <input type="text" v-model="addText" v-on:keyup.enter="addTask" />
    <button @click="addTask">追加</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      addText: "",
      todos: [],
    };
  },
  methods: {
    addTask() {
      this.todos.push({ text: this.addText, done: '作業中' });
      this.addText = "";
    },
    deleteTask(index) {
      this.todos.splice(index, 1);
    },
  },
};
</script>