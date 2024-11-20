<script setup lang="ts">
import { ref } from 'vue';

const emit = defineEmits<{
    (e: 'submit', text: string, tags: string[]): void
}>();

const text = ref("");
const tags = ref<string[]>([]);

function onSubmit() {
    const tags = [...text.value.matchAll(/#\S*/g)].map(v => v[0].slice(1));
    emit('submit', text.value, tags);
    text.value = '';
    tags.value = [];
}
</script>

<template>
    <article class="card bg-base-100 shadow-xl w-full aspect-square relative">
        <form
            class="card-body p-0"
            @submit.prevent="onSubmit"
            @keypress.enter.prevent="onSubmit"
            @keypress="onKeypress"
        >
            <textarea
                class="textarea p-8 h-full"
                placeholder="Insira sua anotação"
                autofocus
                style="resize: none"
                v-model="text"
            ></textarea>
            <button type="submit" class="btn btn-primary absolute bottom-4 right-4">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                    <path stroke-linecap="round" stroke-linejoin="round" d="m4.5 12.75 6 6 9-13.5" />
                </svg>
            </button>
        </form>
    </article>
</template>
