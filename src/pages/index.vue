<script setup lang="ts">
import { useMutation, useQuery } from "@vue/apollo-composable";
// import boardsQuery from "@/graphql/queries/boards.query.gql";
import { computed } from "vue";

// const { result, loading, onError } = useQuery(boardsQuery);
// const boards = computed(() => result.value?.boardsList?.items || []);

// async function handleBoardCreate() {
//   const newBoardPayload = {
//     data: {
//       title: "My New Board",
//     },
//   };
//   await createBoard(newBoardPayload);
//   alerts.success("New Board created!");
// }

const boards = [
  {
    id: 1,
    image: "",
    title: "Title"
  },
];
</script>
<template>
  <Navigation></Navigation>
  <div class="flex">
    <Sidebar></Sidebar>
    <div class="boards p-4">
      <h1 class="mb-5 text-3xl">Boards</h1>
      <div class="flex flex-wrap gap-2">
        <!--         :class="getCoolGradient(index)" -->
        <div
          class="border rounded-md bg-gradient-to-tr"
          v-for="(board) in boards"
          :key="board.id"
        >
          <BoardCard
            :board="board"
            class="transition duration-100 ease-in border rounded-md hover:-rotate-3"
          />
        </div>
        <!--  @click="handleBoardCreate" -->
        <button class="text-gray-500">
          <span>New Board +</span>
        </button>
      </div>
      <!-- <AppLoader v-if="loading" :overlay="true" /> -->
    </div>
  </div>
</template>
