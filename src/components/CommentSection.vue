<script setup>
import { computed } from 'vue'

const props = defineProps({
})

</script>

<template>
    <div class="comic-comments mt-6 bg-gray-200 h-96 rounded-lg flex justify-center items-center">
        <button class="bg-gray-50 ring-1 ring-gray-500/10 ring-inset flex items-center gap-2 rounded-lg px-6 py-2">
            <svg xmlns="http://www.w3.org/2000/svg" width="28" height="28" viewBox="0 0 24 24" fill="none"
                stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                class="icon icon-tabler icons-tabler-outline icon-tabler-messages">
                <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                <path d="M21 14l-3 -3h-7a1 1 0 0 1 -1 -1v-6a1 1 0 0 1 1 -1h9a1 1 0 0 1 1 1v10" />
                <path d="M14 15v2a1 1 0 0 1 -1 1h-7l-3 3v-10a1 1 0 0 1 1 -1h2" />
            </svg>
            <span class="text-lg font-semibold">Click to load comments</span>
        </button>
    </div>
</template>