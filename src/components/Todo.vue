<script>
import check from "../assets/icon-check.svg";
import cross from "../assets/icon-cross.svg";

export default {
  props: {
    todo: {
      type: Object,
      required: true,
    },
    index: {
      type: Number,
      required: true,
    },
    onCheck: {
      type: Function,
      required: true,
    },
    removeTodo: {
      type: Function,
      required: true,
    },
  },
  components: { check, cross },
};
</script>

<template>
  <div v-if="todo.checked" class="flex items-center justify-between flex-1">
    <div
      @click="onCheck(index)"
      class="flex cursor-pointer items-center justify-center gap-4"
    >
      <div
        class="flex items-center justify-center w-6 h-6 rounded-full todoCircle"
      >
        <check class="icon" />
      </div>
      <p class="text-gray-500 line-through">{{ todo.text }}</p>
    </div>
    <div @click="removeTodo(index)" class="cursor-pointer close">
      <span class="close__first" />
      <span class="close__second" />
    </div>
  </div>

  <div
    v-else
    @click="onCheck(index)"
    class="flex items-center justify-between flex-1"
  >
    <div class="flex cursor-pointer items-center justify-center gap-4">
      <div class="svg-wrapper notCheckedTodoCircle" />
      <p>{{ todo.text }}</p>
    </div>
  </div>
</template>
<style scoped>
.icon {
  display: flex;
  justify-content: center;
  align-content: center;
}
.svg-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
