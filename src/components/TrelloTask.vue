<script setup lang="ts">
defineProps<{
  task: Task;
}>();
</script>

<template>
  <div
    class="bg-white rounded shadow min-w-[250px] p-2 mb-2"
    :title="task.content"
  >
    <input
      @key.enter="($event.target as HTMLInputElement).blur()"
      v-model="task.title"
      type="text"
    />
    <!-- {{ task.title }} -->
  </div>
</template>

<style scoped></style>
