<template>
  <div>
    <h1>To Do リスト</h1>
    <form>
      <label v-for="option in options" :key="option.label">
        <input type="radio" v-model="current" v-bind:value="option.label" />
        {{ option.label }}
      </label>
    </form>
    <table>
      <tr>
        <th>ID</th>
        <th>コメント</th>
        <th>状態</th>
      </tr>
      <tr v-for="(todo, index) in filteredTodos" :key="todo">
        <td>{{ index }}</td>
        <td>{{ todo.text }}</td>
        <td>
          <button @click="stateTask(index)">{{ todo.state }}</button>
        </td>
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
      current: "すべて",
      options: [
        {label: "すべて" },
        {label: "作業中" },
        {label: "完了" },
      ],
    };
  },
  computed: {
    filteredTodos() {
      return this.todos.filter(function (todo) {
        return this.current === "すべて" ? true : this.current === todo.state;
      }, this);
    },
  },
  methods: {
    addTask() {
      this.todos.push({ text: this.addText, state: "作業中" });
      this.addText = "";
    },
    deleteTask(index) {
      this.todos.splice(index, 1);
    },
    stateTask(index) {
      if (this.todos[index].state === "作業中") {
        this.todos[index].state = "完了";
      } else {
        this.todos[index].state = "作業中";
      }
    },
  },
};
</script>