<script setup lang="ts">
import { ref } from 'vue';
import Card from './components/Card.vue';
import CardCreate from './components/CardCreate.vue';

const notes = ref<Note[]>([
  {
    id: '1',
    text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Nihil accusamus, adipisci cum pariatur dolor totam. Maiores saepe, eaque voluptates reprehenderit debitis id perspiciatis totam ipsum illo in quisquam minima adipisci.',
    tags: [
      'ideas',
      'game',
    ]
  }
]);

function handleSubmitCardCreate(text: string, tags: string[]) {
  notes.value.push({
    id: Date.now().toString(),
    text: text,
    tags: tags
  });
}

</script>

<template>
  <nav class="navbar bg-base-100 sticky top-0 z-10">
    <div class="flex-none">
      <button class="btn btn-square btn-ghost">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
          class="inline-block h-5 w-5 stroke-current">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
        </svg>
      </button>
    </div>
    <div class="flex-1">
      <a class="btn btn-ghost text-xl">V-Notes</a>
    </div>
    <div class="flex-none">
      <button class="btn btn-square btn-ghost">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
          class="inline-block h-5 w-5 stroke-current">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
            d="M5 12h.01M12 12h.01M19 12h.01M6 12a1 1 0 11-2 0 1 1 0 012 0zm7 0a1 1 0 11-2 0 1 1 0 012 0zm7 0a1 1 0 11-2 0 1 1 0 012 0z">
          </path>
        </svg>
      </button>
    </div>
  </nav>
  <main class="p-4 grid xs:grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-4">
    <CardCreate @submit="handleSubmitCardCreate" />
    <Card v-for="note in notes" :key="note.id" :text="note.text" :tags="note.tags" />
  </main>
</template>
