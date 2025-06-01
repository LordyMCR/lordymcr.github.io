<script setup>
import { ref } from 'vue';

const projects = [
    {
        title: 'Project One',
        description: 'A modern web app built with Laravel and Vue.',
        image: 'https://placehold.co/600x400?text=Project+1',
        video: '', // Optionally add a video/gif URL
    },
    {
        title: 'Project Two',
        description: 'A feature-rich dashboard for analytics.',
        image: 'https://placehold.co/600x400?text=Project+2',
        video: '',
    },
    {
        title: 'Project Three',
        description: 'A beautiful landing page with animations.',
        image: 'https://placehold.co/600x400?text=Project+3',
        video: '',
    },
];

const current = ref(0);

function prev() {
    current.value = (current.value - 1 + projects.length) % projects.length;
}
function next() {
    current.value = (current.value + 1) % projects.length;
}
</script>

<template>
    <div class="relative w-full max-w-3xl mx-auto">
        <div class="overflow-hidden rounded-xl shadow-lg bg-white dark:bg-gray-700">
            <div class="flex items-center justify-center h-80 bg-gray-100 dark:bg-gray-700">
                <template v-if="projects[current].video">
                    <video :src="projects[current].video" class="h-full w-full object-cover" autoplay loop muted playsinline />
                </template>
                <template v-else>
                    <img :src="projects[current].image" :alt="projects[current].title" class="h-full w-full object-cover" />
                </template>
            </div>
            <div class="p-6 text-center">
                <h3 class="text-xl font-bold mb-2">{{ projects[current].title }}</h3>
                <p class="text-gray-600 dark:text-gray-300">{{ projects[current].description }}</p>
            </div>
        </div>
        <!-- Arrows -->
        <button @click="prev" class="absolute left-0 top-1/2 -translate-y-1/2 bg-white/80 dark:bg-gray-900/80 rounded-full p-2 shadow hover:bg-blue-100 dark:hover:bg-blue-900 transition">
            <span class="sr-only">Previous</span>
            <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7" /></svg>
        </button>
        <button @click="next" class="absolute right-0 top-1/2 -translate-y-1/2 bg-white/80 dark:bg-gray-900/80 rounded-full p-2 shadow hover:bg-blue-100 dark:hover:bg-blue-900 transition">
            <span class="sr-only">Next</span>
            <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9 5l7 7-7 7" /></svg>
        </button>
        <!-- Dots -->
        <div class="flex justify-center mt-4 gap-2">
            <button v-for="(p, i) in projects" :key="i" @click="current = i" :class="['w-3 h-3 rounded-full', i === current ? 'bg-blue-600' : 'bg-gray-400 dark:bg-gray-700']" />
        </div>
    </div>
</template> 