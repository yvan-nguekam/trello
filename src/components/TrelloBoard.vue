<script setup lang="ts">
import { ref, watch } from "vue";
import type { Column } from "@/types";
import Draggable from "vuedraggable";
import TrelloTask from "./TrelloTask.vue";
import { useLocalStorage } from "@vueuse/core";

const columns = useLocalStorage<Array<Column>>("trello-board", [
  {
    id: 1,
    title: "Upcoming",
    tasks: [
      {
        id: 1,
        title: "Créer une application frontend",
        content: "Développer une application avec Vue 3 et API Composition",
      },
      {
        id: 2,
        title: "Créer une application backend",
        content: "Développer une application avec laravel 11",
      },
    ],
  },
  {
    id: 2,
    title: "To Do",
    tasks: [],
  },
  {
    id: 3,
    title: "Done",
    tasks: [],
  },
]);

watch(
  columns,
  () => {
    // CALL TO API
  },
  { immediate: true }
);
</script>

<template lang="">
  <Draggable
    v-model="columns"
    group="columns"
    item-key="id"
    :animation="150"
    handle=".cursor-grab"
    class="flex items-start mt-10 space-x-4"
  >
    <template #item="{ element: column }: { element: Column }">
      <div class="bg-gray-50 rounded shadow min-w-[250px] p-5">
        <div class="flex mr-1">
          <span class="cursor-grab">*</span>
          <header class="mb-5 font-bold">{{ column.title }}</header>
        </div>
        <Draggable v-model="column.tasks" group="tasks" item-key="id">
          <template #item="{ element: task }: { element: Task }">
            <TrelloTask :task="task" />
          </template>
        </Draggable>

        <!-- <div
          v-for="task in column.tasks"
          class="bg-white rounded shadow min-w-[250px] p-2 mb-2"
          :title="task.content"
        >
          {{ task.title }}
        </div> -->
      </div>
    </template>
  </Draggable>
</template>

<style></style>
