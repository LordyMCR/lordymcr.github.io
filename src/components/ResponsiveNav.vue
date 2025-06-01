<script setup>
import { ref, onMounted, watch } from 'vue';

const props = defineProps({
    isDark: Boolean,
    toggleDark: Function,
});

const menuOpen = ref(false);
const sections = [
    { id: 'home', label: 'Home' },
    { id: 'about', label: 'About' },
    { id: 'experience', label: 'Experience' },
    { id: 'projects', label: 'Projects' },
    { id: 'education', label: 'Education' },
    { id: 'contact', label: 'Contact' },
];
const activeSection = ref('home');

function scrollToSection(id) {
    const el = document.getElementById(id);
    if (el) {
        el.scrollIntoView({ behavior: 'smooth' });
        menuOpen.value = false;
    }
}

function onScroll() {
    // Highlight the section currently in view
    const offsets = sections.map(s => {
        const el = document.getElementById(s.id);
        if (!el) return { id: s.id, top: Infinity };
        return { id: s.id, top: el.getBoundingClientRect().top };
    });
    const inView = offsets.filter(o => o.top <= 80).sort((a, b) => b.top - a.top);
    if (inView.length) activeSection.value = inView[0].id;
}

onMounted(() => {
    window.addEventListener('scroll', onScroll, { passive: true });
});

watch(menuOpen, (open) => {
    if (open) {
        document.body.style.overflow = 'hidden';
    } else {
        document.body.style.overflow = '';
    }
});
</script>

<template>
    <nav class="sticky top-0 z-50 w-full bg-white/80 dark:bg-gray-900 backdrop-blur shadow flex items-center justify-between px-4 py-3">
        <!-- Mobile: Burger left, name center, dark mode right -->
        <div class="flex items-center w-full md:hidden">
            <!-- Burger -->
            <button class="p-2 rounded focus:outline-none focus:ring-2 focus:ring-blue-400" @click="menuOpen = true" aria-label="Open menu">
                <svg v-if="!menuOpen" class="w-7 h-7 text-gray-900 dark:text-white" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M4 6h16M4 12h16M4 18h16"/></svg>
            </button>
            <!-- Name center -->
            <div class="flex-1 flex justify-center">
                <div class="font-bold text-xl text-gray-900 dark:text-white select-none cursor-pointer" @click="scrollToSection('home')">
                    Daniel Lord
                </div>
            </div>
            <!-- Dark mode toggle right -->
            <div class="flex items-center">
                <slot />
            </div>
        </div>
        <!-- Desktop nav -->
        <div class="hidden md:flex w-full items-center justify-between">
            <div class="font-bold text-xl text-gray-900 dark:text-white select-none cursor-pointer" @click="scrollToSection('home')">
                Daniel Lord
            </div>
            <ul class="flex gap-8 text-lg font-semibold">
                <li v-for="s in sections" :key="s.id">
                    <button
                        type="button"
                        @click="scrollToSection(s.id)"
                        :class="[
                            'transition-colors duration-200 focus:outline-none',
                            activeSection === s.id
                                ? 'text-blue-600 dark:text-blue-400 underline underline-offset-4'
                                : 'hover:text-blue-600 dark:hover:text-blue-400 text-gray-900 dark:text-white'
                        ]"
                    >
                        {{ s.label }}
                    </button>
                </li>
            </ul>
            <div class="flex items-center gap-2 ml-4">
                <slot />
            </div>
        </div>
    </nav>
    <!-- Mobile nav menu rendered in <body> so it doesn't affect sticky nav -->
    <teleport to="body">
        <div v-if="menuOpen" class="fixed inset-0 z-50 flex flex-col bg-white dark:bg-gray-900">
            <!-- Close icon -->
            <button class="absolute top-4 right-4 p-2 rounded focus:outline-none focus:ring-2 focus:ring-blue-400" @click="menuOpen = false" aria-label="Close menu">
                <svg class="w-7 h-7 text-gray-900 dark:text-white" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12"/></svg>
            </button>
            <div class="flex-1 flex flex-col justify-center items-center gap-8">
                <div class="font-bold text-2xl mb-2 text-gray-900 dark:text-white underline">Menu</div>
                <button v-for="s in sections" :key="s.id" @click="scrollToSection(s.id)" :class="[
                    'text-2xl font-semibold py-2 px-4 rounded transition-colors w-full text-center',
                    activeSection === s.id
                        ? 'text-blue-600 dark:text-blue-400 bg-blue-50 dark:bg-gray-800'
                        : 'hover:text-blue-600 dark:hover:text-blue-400 text-gray-900 dark:text-white'
                ]">
                    {{ s.label }}
                </button>
                <div class="mt-8">
                    <slot name="mobile-extra" />
                </div>
            </div>
        </div>
    </teleport>
</template>

<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.2s;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style> 