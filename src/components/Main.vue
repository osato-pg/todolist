<template>
  <div>
    <h1>To Do リスト</h1>
    <form>
      <label v-for="label in options" :key="label.value">
        <input type="radio" v-model="current" v-bind:value="label.value" />
        {{ label.label }}
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
          <button @click="stateTask(index)">{{ labels[todo.state] }}</button>
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
      current: -1,
      options: [
        { value: -1, label: "すべて" },
        { value: 0, label: "作業中" },
        { value: 1, label: "完了" },
      ],
    };
  },
  computed: {
    filteredTodos() {
      return this.todos.filter(function (todo) {
        return this.current < 0 ? true : this.current === todo.state;
      }, this);
    },
    labels() {
      return this.options.reduce(function (a, b) {
        return Object.assign(a, { [b.value]: b.label });
      }, {});
    },
  },
  methods: {
    addTask() {
      this.todos.push({ text: this.addText, state: 0 });
      this.addText = "";
    },
    deleteTask(index) {
      this.todos.splice(index, 1);
    },
    stateTask(index) {
      if (this.todos[index].state === 0) {
        this.todos[index].state = 1;
      } else {
        this.todos[index].state = 0;
      }
    },
  },
};
</script>