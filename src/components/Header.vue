<script>
import Moon from "../assets/icon-moon.svg";
import Sun from "../assets/icon-sun.svg";

export default {
  props: ["isInDarkMode", "toggleDarkMode", "Icon"],
  components: {Moon, Sun},
};
</script>

<template>
  <header class="flex justify-between">
    <h1 class="text-5xl font-bold tracking-[0.3em] text-gray-50">TODO</h1>
    <button v-if="isInDarkMode" class="fill-red-100" @click="toggleDarkMode">
      <Sun class="fill-icons" />
    </button>
    <button v-else @click="toggleDarkMode">
      <Moon class="fill-icons" />
    </button>
  </header>
</template>

<style>
</style>
