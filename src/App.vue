<template>
  <div class="max-w-4xl mx-auto border-2 border-solid border-black flex flex-col justify-center mt-10">
    <img src="./assets/to-do-list-logo.svg" alt="to do list icon" class=" w-16 h-16 mt-4 mx-auto"   />
    <div>
      <TodoList />
    </div>
  </div>
  <i class="ml-72 text-green-500">N.b, double click an item to edit</i>
</template>

<script>
  import TodoList from './components/TodoList.vue';
  export default {
    components: {
      TodoList
    }
  }
</script>

<style>

</style>