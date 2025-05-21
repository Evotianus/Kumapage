<script setup>
import { computed } from 'vue'
import dayjs from 'dayjs'

const props = defineProps({
    number: Number,
    date: [Date, String],
})

const formattedDate = computed(() => {
    if (!props.date) return '';
    return dayjs(props.date).format('MMM D, YYYY');
})
</script>

<template>
    <div class="bg-gray-50 ring-1 ring-gray-500/10 ring-inset rounded-lg p-2 flex items-center">
        <div class="flex items-center gap-4">
            <img src="https://assets.bwbx.io/images/users/iqjWHBFdfxIU/ixfNTiyYtG1c/v0/459x306.webp" alt=""
                class="h-full w-36 rounded-lg">
            <div class="flex flex-col">
                <p class="font-semibold text-lg">Chapter {{ number }}</p>
                <span>{{ formattedDate }}</span>
            </div>
        </div>
    </div>
</template>