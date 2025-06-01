<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const sections = [
    { id: 'home', label: 'Home' },
    { id: 'about', label: 'About' },
    { id: 'experience', label: 'Experience' },
    { id: 'projects', label: 'Projects' },
    { id: 'education', label: 'Education' },
    { id: 'contact', label: 'Contact' },
];
const currentSection = ref(0);

function scrollToSection(idx) {
    const el = document.getElementById(sections[idx].id);
    if (el) {
        el.scrollIntoView({ behavior: 'smooth' });
    }
}

function updateCurrentSection() {
    const offsets = sections.map((s) => {
        const el = document.getElementById(s.id);
        if (!el) return { id: s.id, top: Infinity };
        return { id: s.id, top: el.getBoundingClientRect().top };
    });
    const inView = offsets.filter((o) => o.top <= 80).sort((a, b) => b.top - a.top);
    if (inView.length) {
        currentSection.value = sections.findIndex((s) => s.id === inView[0].id);
    }
}

onMounted(() => {
    window.addEventListener('scroll', updateCurrentSection, { passive: true });
    updateCurrentSection();
});
onUnmounted(() => {
    window.removeEventListener('scroll', updateCurrentSection);
});
</script>

<template>
    <!-- Up Arrow -->
    <button
        v-if="currentSection > 0"
        @click="scrollToSection(currentSection - 1)"
        class="fixed right-4 top-24 z-40 bg-white dark:bg-gray-700 text-gray-900 dark:text-white border border-gray-300 dark:border-gray-700 rounded-full shadow-xl p-3 md:p-4 hover:bg-gray-100 dark:hover:bg-gray-800 transition focus:outline-none focus:ring-2 focus:ring-blue-400"
        aria-label="Scroll to previous section"
    >
        <svg class="w-7 h-7" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M5 15l7-7 7 7"/></svg>
    </button>
    <!-- Down Arrow -->
    <button
        v-if="currentSection < sections.length - 1"
        @click="scrollToSection(currentSection + 1)"
        class="fixed right-4 bottom-4 z-40 bg-gray-50 dark:bg-gray-800 text-gray-900 dark:text-white border border-gray-300 dark:border-gray-700 rounded-full shadow-xl p-3 md:p-4 hover:bg-gray-100 dark:hover:bg-gray-700 transition focus:outline-none focus:ring-2 focus:ring-blue-400"
        aria-label="Scroll to next section"
    >
        <svg class="w-7 h-7" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7"/></svg>
    </button>
</template> 