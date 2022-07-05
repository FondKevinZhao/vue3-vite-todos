<template>
  <div>
    <h1>App根组件</h1>
    <hr />
    <TodoInput @add="onAddNewTask"></TodoInput>
    <TodoList :list="tasklist" class="mt-2"></TodoList>
    <TodoButton v-model:active="activeBtnIndex"></TodoButton>
  </div>
</template>

<script>
import TodoList from "./components/todo-list/TodoList.vue";
import TodoInput from "./components/todo-input/TodoInput.vue";
import TodoButton from "./components/todo-button/TodoButton.vue";
export default {
  name: "MyApp",
  data() {
    return {
      todolist: [
        { id: 1, task: "周一早晨9点开会", done: false },
        { id: 2, task: "周一晚上8点聚餐", done: false },
        { id: 3, task: "准备周三上午的演讲稿", done: true },
      ],
      nextId: 4, // 下一个可用的id
      activeBtnIndex: 0, // 默认选择为0
    };
  },
  components: {
    TodoList,
    TodoInput,
    TodoButton,
  },
  methods: {
    onAddNewTask(taskname) {
      this.todolist.push({
        id: this.nextId,
        task: taskname,
        done: false,
      });
      this.nextId++;
    },
  },
  computed: {
    // 最终切换：全部 已完成 未完成
    tasklist() {
      switch (this.activeBtnIndex) {
        case 0:
          return this.todolist;
        case 1:
          return this.todolist.filter((item) => item.done === true);
        case 2:
          return this.todolist.filter((item) => item.done !== true);
      }
    },
  },
};
</script>

<style lang="less" scoped>
</style>
