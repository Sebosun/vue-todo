<script>
import Todo from "./components/Todo.vue";
import Header from "./components/Header.vue";
import TabSwitchMenu from "./components/TabSwitchMenu.vue";

import draggable from "vuedraggable";
let id = 5;
export default {
  data() {
    return {
      message: "",
      isInDarkMode: false,
      counter: 0,
      todos: [
        {
          text: "Complete online JavaScript course",
          checked: true,
          id: 0,
        },
        {
          text: "Jog around the park 3x",
          checked: false,
          id: 1,
        },
        {
          text: "10 minutes meditation",
          checked: false,
          id: 2,
        },
        {
          text: "Read for 1 hour",
          checked: false,
          id: 3,
        },
        {
          text: "Pick up groceries",
          checked: false,
          id: 4,
        },
        {
          text: "Complete Todo App on Frontend Mentor",
          checked: false,
          id: 5,
        },
      ],
      drag: false,
      styleObject: {
        color: "red",
        fontSize: "13px",
      },
    };
  },
  methods: {
    add() {
      this.counter = this.counter + 1;
    },
    toggleDarkMode() {
      if (this.isInDarkMode) {
        document.documentElement.classList.remove("dark");
        document.documentElement.classList.remove("bg-gray-900");
        this.isInDarkMode = !this.isInDarkMode;
      } else {
        document.documentElement.classList.add("dark");
        document.documentElement.classList.add("bg-gray-900");
        this.isInDarkMode = !this.isInDarkMode;
      }
    },
    onCheck(id) {
      const index = this.todos.findIndex((el) => el.id == id);
      this.todos[index].checked = !this.todos[index].checked;
    },
    onSubmit() {
      this.todos.push({ text: this.message, checked: false, id: id++ });
      this.message = "";
    },
    removeTodo(id) {
      const index = this.todos.findIndex((el) => el.id == id);
      this.todos.splice(index, 1);
    },
  },
  computed: {
    itemsLength() {
      return this.todos.filter((item) => !item.checked).length;
    },
  },
  components: { draggable, Todo, Header, TabSwitchMenu },
};
</script>

<template>
  <img
    class="w-full h-64 md:h-80 object-cover"
    v-if="!isInDarkMode"
    src="./assets/bg-desktop-light.jpg"
  />
  <img
    class="w-full h-64 object-cover"
    v-else
    src="./assets/bg-desktop-dark.jpg"
  />

  <div
    class="p-4 relative max-w-xl mt-8 md:mt-0 mx-auto dark:text-white bottom-64 drop-shadow-2xl xl:bottom-72"
  >
    <Header :isInDarkMode="isInDarkMode" :toggleDarkMode="toggleDarkMode" />
    <div class="m-42">
      <form @submit.prevent="onSubmit">
        <label
          class="flex w-full gap-3 bg-white dark:bg-[#25274C] p-4 rounded-md my-8"
        >
          <div
            class="flex self-center justify-center w-6 h-6 notCheckedTodoCircle"
          />
          <input
            v-model="message"
            placeholder="Create a new todo"
            class="flex-1 p-1 ring-offset-purple-100 bg-white dark:bg-[#25274C]"
          />
        </label>
      </form>
    </div>

    <main class="flex flex-col">
      <div class="bg-[hsl(0,0%,98%)] rounded-lg shadow-2xl dark:bg-[#25274C]">
        <draggable
          v-model="todos"
          group="todos"
          @start="drag = true"
          @end="drag = false"
          item-key="id"
        >
          <template #item="{ element }">
            <div
              class="todo flex gap-4 items-center p-4 border-b-[1px] border-solid border-[#777A92] dark:text-gray-50"
            >
              <Todo
                :removeTodo="removeTodo"
                :index="element.id"
                :todo="element"
                :onCheck="onCheck"
              />
            </div>
          </template>
        </draggable>

        <div
          class="flex gap-4 md:gap-0 justify-between p-4 text-sm rounded-b-lg"
        >
          <p class="btn">{{ itemsLength }} Items left</p>
          <div class="hidden justify-center align-center md:block flex gap-4">
            <TabSwitchMenu />
          </div>
          <button class="btn">Clear Completed</button>
        </div>
      </div>

      <div
        class="flex md:hidden bg-[hsl(0,0%,98%)] mt-4 p-4 justify-around rounded-lg shadow-2xl dark:bg-[#25274C]"
      >
        <TabSwitchMenu />
      </div>
    </main>

    <p class="my-6 text-xs text-center bottom__text">
      Drag and drop to reorder list
    </p>
  </div>
</template>

<style>
.notDoneTodo {
  width: 2.5rem;
  height: 2.5rem;
  border: 1px solid;
  border-radius: 9999px;
}

.notCheckedTodoCircle {
  width: 1.5rem;
  height: 1.5rem;
  border: 1px solid gray;
  cursor: pointer;
  border-radius: 9999px;
}

.todoCircle {
  background: linear-gradient(hsl(192, 100%, 67%), hsl(280, 87%, 65%));
}

.todos:first-child {
  border-top-left-radius: 1rem;
  border-top-right-radius: 1rem;
}

.close {
  position: relative;
  top: 8px;
}
.close span {
  display: block;
  position: relative;
  height: 2px;
  width: 30px;
  margin-bottom: 6px;
  background-color: #5d5d67;
}

.close__first {
  transform: rotate(50deg);
}
.close__second {
  transform: rotate(-50deg);
  top: -8px;
}

.bottom__text {
  color: hsl(233, 14%, 35%);
}

.btn {
  color: hsl(234, 11%, 52%);
}

.btn:hover {
  color: hsl(236, 33%, 92%);
}

.active {
  font-weight: 700;
  color: hsl(220, 98%, 61%);
}
</style>
