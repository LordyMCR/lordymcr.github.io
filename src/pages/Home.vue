<script setup>
import { ref, onMounted } from 'vue';
import ProjectCarousel from '../components/ProjectCarousel.vue';
import ResponsiveNav from '../components/ResponsiveNav.vue';
import SectionNavArrows from '../components/SectionNavArrows.vue';
import ExperienceCarousel from '../components/ExperienceCarousel.vue';

const isDark = ref(false);

function setDarkMode(val) {
    isDark.value = val;
    document.documentElement.classList.toggle('dark', val);
    localStorage.setItem('theme', val ? 'dark' : 'light');
}

function toggleDark() {
    setDarkMode(!isDark.value);
}

// Auto-calculate age from birthday (25/07/1994)
function calculateAge(birthdayStr) {
    const today = new Date();
    const birthday = new Date(birthdayStr);
    let age = today.getFullYear() - birthday.getFullYear();
    const m = today.getMonth() - birthday.getMonth();
    if (m < 0 || (m === 0 && today.getDate() < birthday.getDate())) {
        age--;
    }
    return age;
}
const age = calculateAge('1994-07-25');

// Dark mode toggle
onMounted(() => {
    const saved = localStorage.getItem('theme');
    if (saved === 'dark' || (!saved && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
        setDarkMode(true);
    } else {
        setDarkMode(false);
    }
});
</script>

<template>
    <ResponsiveNav :isDark="isDark" :toggleDark="toggleDark">
        <template #default>
            <button @click="toggleDark" class="ml-4 p-2 rounded-full bg-gray-200 dark:bg-gray-700 hover:bg-gray-300 dark:hover:bg-gray-600 transition shadow" aria-label="Toggle dark mode">
                <svg v-if="!isDark" class="w-6 h-6 text-yellow-500" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><circle cx="12" cy="12" r="5"/><path d="M12 1v2m0 18v2m11-11h-2M3 12H1m16.95 7.07-1.41-1.41M6.34 6.34 4.93 4.93m12.02 0-1.41 1.41M6.34 17.66l-1.41 1.41"/></svg>
                <svg v-else class="w-6 h-6 text-gray-200" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M21 12.79A9 9 0 1111.21 3a7 7 0 109.79 9.79z"/></svg>
            </button>
        </template>
    </ResponsiveNav>

    <main>
        <section id="home" class="min-h-screen flex items-center justify-center bg-gradient-to-b from-white to-gray-100 dark:from-gray-800 dark:to-gray-700 text-center text-gray-900 dark:text-white">
            <div class="w-full max-w-2xl px-2 sm:px-4 flex flex-col items-center gap-6 sm:gap-8 py-10 sm:py-16">
                <img
                    src="/images/profile-cropped.png"
                    alt="Daniel Lord profile photo"
                    class="w-32 h-32 sm:w-48 sm:h-48 rounded-full object-cover shadow-2xl mb-2"
                />
                <h1 class="text-2xl sm:text-4xl md:text-5xl font-extrabold tracking-tight mb-2">Daniel Lord</h1>
                <h2 class="text-base sm:text-xl md:text-2xl font-semibold text-blue-600 dark:text-blue-400 mb-2 sm:mb-4">
                    Full Stack Developer • Software Engineer • Award-Winning Graduate
                </h2>
                <p class="text-base sm:text-lg md:text-xl leading-relaxed mb-2 sm:mb-4">
                    I'm a highly focused and driven full stack developer with First Class Honours and award-winning results. I have 2+ years of professional experience building modern web and mobile applications using Laravel, Vue, React Native, and more. I thrive on solving complex problems, delivering user-friendly solutions, and collaborating in both team and independent environments.
                </p>
                <div class="flex flex-wrap justify-center gap-2 sm:gap-4 mt-2">
                    <a href="https://linkedin.com/in/daniel-lord-b83b71a7" target="_blank" rel="noopener" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-blue-100 dark:bg-blue-900 text-blue-700 dark:text-blue-300 font-semibold shadow hover:bg-blue-200 dark:hover:bg-blue-800 transition">
                        <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M19 0h-14c-2.76 0-5 2.24-5 5v14c0 2.76 2.24 5 5 5h14c2.76 0 5-2.24 5-5v-14c0-2.76-2.24-5-5-5zm-11 19h-3v-10h3v10zm-1.5-11.28c-.97 0-1.75-.79-1.75-1.75s.78-1.75 1.75-1.75 1.75.79 1.75 1.75-.78 1.75-1.75 1.75zm15.5 11.28h-3v-5.6c0-1.34-.03-3.07-1.87-3.07-1.87 0-2.16 1.46-2.16 2.97v5.7h-3v-10h2.88v1.36h.04c.4-.75 1.38-1.54 2.84-1.54 3.04 0 3.6 2 3.6 4.59v5.59z"/></svg>
                        LinkedIn
                    </a>
                    <a href="https://github.com/LordyMCR" target="_blank" rel="noopener" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-gray-100 dark:bg-gray-800 text-gray-900 dark:text-white font-semibold shadow hover:bg-gray-200 dark:hover:bg-gray-700 transition">
                        <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M12 0c-6.63 0-12 5.37-12 12 0 5.3 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61-.546-1.387-1.333-1.756-1.333-1.756-1.09-.745.083-.729.083-.729 1.205.085 1.84 1.237 1.84 1.237 1.07 1.834 2.807 1.304 3.492.997.108-.775.418-1.305.762-1.605-2.665-.305-5.466-1.332-5.466-5.93 0-1.31.47-2.38 1.236-3.22-.124-.303-.535-1.523.117-3.176 0 0 1.008-.322 3.3 1.23.96-.267 1.98-.399 3-.404 1.02.005 2.04.137 3 .404 2.29-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.873.12 3.176.77.84 1.235 1.91 1.235 3.22 0 4.61-2.803 5.624-5.475 5.921.43.372.823 1.102.823 2.222 0 1.606-.015 2.898-.015 3.293 0 .322.216.694.825.576 4.765-1.587 8.2-6.086 8.2-11.384 0-6.63-5.373-12-12-12z"/></svg>
                        GitHub
                    </a>
                    <a href="mailto:daniel.lord13@outlook.com" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-green-100 dark:bg-green-900 text-green-700 dark:text-green-300 font-semibold shadow hover:bg-green-200 dark:hover:bg-green-800 transition">
                        <svg class="w-5 h-5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M16 12H8m8 0l-4-4m4 4l-4 4"/></svg>
                        Email
                    </a>
                </div>
            </div>
        </section>

        <section id="about" class="relative min-h-screen flex items-center justify-center bg-gradient-to-b from-green-50 to-teal-100 dark:from-green-900 dark:to-teal-900 text-center text-gray-900 dark:text-white">
          <div aria-hidden="true" class="absolute left-0 top-0 w-full h-full">
            <svg width="100%" height="100%" class="w-full h-full block dark:hidden" fill="none" xmlns="http://www.w3.org/2000/svg">
              <defs>
                <pattern id="diagonal-lines-light" patternUnits="userSpaceOnUse" width="40" height="40" patternTransform="rotate(45)">
                  <rect x="0" y="0" width="20" height="2" fill="#a7f3d0" fill-opacity="0.4" />
                </pattern>
              </defs>
              <rect width="100%" height="100%" fill="url(#diagonal-lines-light)" />
            </svg>
            <svg width="100%" height="100%" class="w-full h-full hidden dark:block" fill="none" xmlns="http://www.w3.org/2000/svg">
              <defs>
                <pattern id="diagonal-lines-dark" patternUnits="userSpaceOnUse" width="40" height="40" patternTransform="rotate(45)">
                  <rect x="0" y="0" width="20" height="2" fill="#065f46" fill-opacity="0.2" />
                </pattern>
              </defs>
              <rect width="100%" height="100%" fill="url(#diagonal-lines-dark)" />
            </svg>
          </div>
          <div class="max-w-3xl px-2 sm:px-4 flex flex-col gap-6 sm:gap-10 py-10 sm:py-16 mx-auto relative z-10">
            <div class="text-center">
                <h2 class="text-xl sm:text-4xl font-bold mb-2 sm:mb-6">About Me</h2>
                <p class="text-sm sm:text-base md:text-xl mb-1 sm:mb-2">
                    Hi, I'm <span class="font-semibold">Daniel Lord</span>, a <span class="font-semibold">{{ age }}</span>-year-old full stack developer based in 
                    <a
                      href="https://www.google.com/maps/place/New+Islington,+Manchester/"
                      target="_blank"
                      rel="noopener"
                      class="inline-flex items-center gap-1 text-blue-600 dark:text-blue-400 hover:underline font-semibold"
                    >
                      <svg class="w-4 h-4 sm:w-5 sm:h-5 inline" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M12 21c-4.418 0-8-4.03-8-9a8 8 0 1116 0c0 4.97-3.582 9-8 9z"/>
                        <circle cx="12" cy="12" r="3" />
                      </svg>
                      New Islington, Manchester City Centre, United Kingdom
                    </a>.
                </p>
            </div>
            <div class="flex flex-wrap justify-center gap-4 sm:gap-8 items-center mt-4 sm:mt-6">
                <div class="flex flex-col items-center min-w-[90px]">
                    <div class="bg-blue-100 dark:bg-blue-900 p-2 sm:p-4 rounded-full mb-1 sm:mb-2">
                        <svg class="w-5 h-5 sm:w-7 sm:h-7 text-blue-600 dark:text-blue-300" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M4 7V6a2 2 0 012-2h12a2 2 0 012 2v1"/><rect width="20" height="13" x="2" y="7" rx="2"/><path stroke-linecap="round" stroke-linejoin="round" d="M16 21v-4a2 2 0 00-2-2H10a2 2 0 00-2 2v4"/></svg>
                    </div>
                    <div class="font-semibold text-sm sm:text-base">2013–2019</div>
                    <div class="text-gray-600 dark:text-gray-400 text-xs sm:text-sm text-center">IT Apprentice & Data Admin</div>
                </div>
                <div class="flex flex-col items-center min-w-[90px]">
                    <div class="bg-green-100 dark:bg-green-900 p-2 sm:p-4 rounded-full mb-1 sm:mb-2">
                        <svg class="w-5 h-5 sm:w-7 sm:h-7 text-green-600 dark:text-green-300" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M12 14l9-5-9-5-9 5 9 5z"/><path stroke-linecap="round" stroke-linejoin="round" d="M12 14l6.16-3.422A12.083 12.083 0 0121 13.5c0 2.485-4.03 4.5-9 4.5s-9-2.015-9-4.5c0-.538.214-1.05.84-1.922L12 14z"/></svg>
                    </div>
                    <div class="font-semibold text-sm sm:text-base">2019–2023</div>
                    <div class="text-gray-600 dark:text-gray-400 text-xs sm:text-sm text-center">BSc Software Engineering<br/>First Class Honours</div>
                </div>
                <div class="flex flex-col items-center min-w-[90px]">
                    <div class="bg-purple-100 dark:bg-purple-900 p-2 sm:p-4 rounded-full mb-1 sm:mb-2">
                        <svg class="w-5 h-5 sm:w-7 sm:h-7 text-purple-600 dark:text-purple-300" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M16 18l6-6-6-6"/><path stroke-linecap="round" stroke-linejoin="round" d="M8 6l-6 6 6 6"/></svg>
                    </div>
                    <div class="font-semibold text-sm sm:text-base">2023–Now</div>
                    <div class="text-gray-600 dark:text-gray-400 text-xs sm:text-sm text-center">Full Stack Developer</div>
                </div>
            </div>
            <div class="flex flex-wrap justify-center gap-4 sm:gap-8 items-center mt-2 sm:mt-4">
                <div class="flex flex-col items-center min-w-[90px]">
                    <div class="text-2xl sm:text-3xl font-bold text-blue-600 dark:text-blue-400">6+</div>
                    <div class="text-xs sm:text-sm text-gray-600 dark:text-gray-400 text-center">Years Professional Experience</div>
                </div>
                <div class="flex flex-col items-center min-w-[90px]">
                    <div class="text-2xl sm:text-3xl font-bold text-green-600 dark:text-green-400">1st</div>
                    <div class="text-xs sm:text-sm text-gray-600 dark:text-gray-400 text-center">Class Honours</div>
                </div>
                <div class="flex flex-col items-center min-w-[90px]">
                    <div class="text-2xl sm:text-3xl font-bold text-purple-600 dark:text-purple-400">2+</div>
                    <div class="text-xs sm:text-sm text-gray-600 dark:text-gray-400 text-center">Years as Developer</div>
                </div>
            </div>
            <div class="text-sm sm:text-base sm:text-xl leading-relaxed text-center mt-1 sm:mt-2">
                After 6 years in IT and data administration, I decided to pursue my passion for software by returning to university. I graduated with First Class Honours in Software Engineering, earning awards for outstanding performance. I'm now working in my first full-time developer role, building modern web and mobile applications as a full stack developer.
            </div>
          </div>
        </section>

        <section id="experience" class="relative min-h-screen w-full flex items-center justify-center bg-gradient-to-b from-blue-50 to-indigo-100 dark:from-blue-900 dark:to-indigo-900 text-center text-gray-900 dark:text-white">
          <div aria-hidden="true" class="absolute left-0 top-0 w-full h-full">
            <svg width="100%" height="100%" class="w-full h-full block dark:hidden" fill="none">
              <defs>
                <pattern id="grid-light" width="40" height="40" patternUnits="userSpaceOnUse">
                  <path d="M 40 0 L 0 0 0 40" fill="none" stroke="#bfdbfe" stroke-width="1"/>
                </pattern>
              </defs>
              <rect width="100%" height="100%" fill="url(#grid-light)" />
            </svg>
            <svg width="100%" height="100%" class="w-full h-full hidden dark:block" fill="none">
              <defs>
                <pattern id="grid-dark" width="40" height="40" patternUnits="userSpaceOnUse">
                  <path d="M 40 0 L 0 0 0 40" fill="none" stroke="#1e3a8a" stroke-width="1"/>
                </pattern>
              </defs>
              <rect width="100%" height="100%" fill="url(#grid-dark)" />
            </svg>
          </div>
          <div class="w-full max-w-4xl mx-auto px-4 relative z-10">
            <h2 class="text-4xl font-bold mb-8">Experience</h2>
            <ExperienceCarousel />
          </div>
        </section>

        <section id="projects" class="min-h-screen w-full flex items-center justify-center bg-gradient-to-b from-white to-gray-100 dark:from-gray-800 dark:to-gray-700 text-center text-gray-900 dark:text-white">
            <div class="w-full max-w-4xl mx-auto px-2 sm:px-4">
                <h2 class="text-2xl sm:text-4xl font-bold mb-4 sm:mb-8">Projects</h2>
                <div class="relative flex items-center justify-center">
                    <button @click="$refs.projectCarousel.prev()" class="hidden md:block p-2 rounded-full bg-gray-100 dark:bg-gray-800 hover:bg-blue-100 dark:hover:bg-blue-900 shadow transition absolute left-0 top-1/2 -translate-y-1/2 z-10" aria-label="Previous">
                        <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7" /></svg>
                    </button>
                    <ProjectCarousel ref="projectCarousel" />
                    <button @click="$refs.projectCarousel.next()" class="hidden md:block p-2 rounded-full bg-gray-100 dark:bg-gray-800 hover:bg-blue-100 dark:hover:bg-blue-900 shadow transition absolute right-0 top-1/2 -translate-y-1/2 z-10" aria-label="Next">
                        <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9 5l7 7-7 7" /></svg>
                    </button>
                </div>
            </div>
        </section>

        <section id="education" class="relative min-h-screen w-full flex items-center justify-center bg-gradient-to-b from-purple-50 to-violet-100 dark:from-purple-900 dark:to-violet-900 text-center text-gray-900 dark:text-white">
          <div aria-hidden="true" class="absolute left-0 top-0 w-full h-full">
            <svg width="100%" height="100%" class="w-full h-full block dark:hidden" fill="none">
              <defs>
                <pattern id="plus-light" width="32" height="32" patternUnits="userSpaceOnUse">
                  <path d="M16 8v16M8 16h16" stroke="#c4b5fd" stroke-width="1"/>
                </pattern>
              </defs>
              <rect width="100%" height="100%" fill="url(#plus-light)" />
            </svg>
            <svg width="100%" height="100%" class="w-full h-full hidden dark:block" fill="none">
              <defs>
                <pattern id="plus-dark" width="32" height="32" patternUnits="userSpaceOnUse">
                  <path d="M16 8v16M8 16h16" stroke="#6d28d9" stroke-width="1"/>
                </pattern>
              </defs>
              <rect width="100%" height="100%" fill="url(#plus-dark)" />
            </svg>
          </div>
          <div class="w-full max-w-4xl mx-auto px-4 flex flex-col items-center relative z-10">
            <h2 class="text-4xl font-bold mb-8 text-center">Education</h2>
            <div class="max-w-2xl w-full mx-auto bg-white dark:bg-gray-800 rounded-2xl shadow-xl p-8 flex flex-col items-center gap-4 border border-gray-200 dark:border-gray-700">
              <img src="/images/man-met-logo.png" alt="Manchester Metropolitan University logo" class="h-14 mb-2 dark:invert dark:brightness-150" />
              <div class="text-2xl font-bold mb-1">BSc (Hons) Software Engineering</div>
              <div class="flex items-center gap-2 text-lg font-semibold text-blue-600 dark:text-blue-400 mb-1">
                <a href="https://www.mmu.ac.uk/" target="_blank" rel="noopener" class="hover:underline flex items-center gap-1">
                  Manchester Metropolitan University
                  <svg class="w-4 h-4 inline text-blue-500 dark:text-blue-300" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M18 13v6a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"/><polyline points="15 3 21 3 21 9"/><line x1="10" y1="14" x2="21" y2="3"/></svg>
                </a>
              </div>
              <div class="text-gray-600 dark:text-gray-400 mb-2">2019–2023</div>
              <div class="inline-block bg-green-100 dark:bg-green-900 text-green-700 dark:text-green-300 px-3 py-1 rounded-full font-semibold text-sm mb-2">
                First Class Honours (89%)
              </div>
              <div class="inline-block bg-purple-100 dark:bg-purple-900 text-purple-700 dark:text-purple-300 px-3 py-1 rounded-full font-semibold text-sm mb-2">
                Award for Outstanding Performance – Software Engineering
              </div>
              <div class="text-base text-center text-gray-700 dark:text-gray-200 mt-2">
                Gained a strong foundation in software engineering principles, modern web development, and collaborative project work. Achieved the highest grade in Software Engineering across the entire cohort, earning the Department's Award for Outstanding Performance.
              </div>
            </div>
          </div>
        </section>
        <section id="contact" class="min-h-screen w-full flex items-center justify-center bg-gradient-to-b from-white to-gray-100 dark:from-gray-800 dark:to-gray-700 text-center text-gray-900 dark:text-white">
          <div class="relative z-10 w-full max-w-4xl mx-auto px-4">
            <div>
                <h2 class="text-4xl font-bold mb-4">Contact Me</h2>
                <p class="text-xl mb-6">Interested in working together, have a question, or just want to say hi? I'd love to hear from you!</p>
                <div class="flex flex-wrap justify-center gap-4 mb-6">
                  <a href="https://linkedin.com/in/daniel-lord-b83b71a7" target="_blank" rel="noopener" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-blue-100 dark:bg-blue-900 text-blue-700 dark:text-blue-300 font-semibold shadow hover:bg-blue-200 dark:hover:bg-blue-800 transition">
                    <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M19 0h-14c-2.76 0-5 2.24-5 5v14c0 2.76 2.24 5 5 5h14c2.76 0 5-2.24 5-5v-14c0-2.76-2.24-5-5-5zm-11 19h-3v-10h3v10zm-1.5-11.28c-.97 0-1.75-.79-1.75-1.75s.78-1.75 1.75-1.75 1.75.79 1.75 1.75-.78 1.75-1.75 1.75zm15.5 11.28h-3v-5.6c0-1.34-.03-3.07-1.87-3.07-1.87 0-2.16 1.46-2.16 2.97v5.7h-3v-10h2.88v1.36h.04c.4-.75 1.38-1.54 2.84-1.54 3.04 0 3.6 2 3.6 4.59v5.59z"/></svg>
                    LinkedIn
                  </a>
                  <a href="https://github.com/LordyMCR" target="_blank" rel="noopener" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-gray-100 dark:bg-gray-800 text-gray-900 dark:text-white font-semibold shadow hover:bg-gray-200 dark:hover:bg-gray-700 transition">
                    <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M12 0c-6.63 0-12 5.37-12 12 0 5.3 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61-.546-1.387-1.333-1.756-1.333-1.756-1.09-.745.083-.729.083-.729 1.205.085 1.84 1.237 1.84 1.237 1.07 1.834 2.807 1.304 3.492.997.108-.775.418-1.305.762-1.605-2.665-.305-5.466-1.332-5.466-5.93 0-1.31.47-2.38 1.236-3.22-.124-.303-.535-1.523.117-3.176 0 0 1.008-.322 3.3 1.23.96-.267 1.98-.399 3-.404 1.02.005 2.04.137 3 .404 2.29-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.873.12 3.176.77.84 1.235 1.91 1.235 3.22 0 4.61-2.803 5.624-5.475 5.921.43.372.823 1.102.823 2.222 0 1.606-.015 2.898-.015 3.293 0 .322.216.694.825.576 4.765-1.587 8.2-6.086 8.2-11.384 0-6.63-5.373-12-12-12z"/></svg>
                    GitHub
                  </a>
                  <a href="mailto:daniel.lord13@outlook.com" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-green-100 dark:bg-green-900 text-green-700 dark:text-green-300 font-semibold shadow hover:bg-green-200 dark:hover:bg-green-800 transition">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M16 12H8m8 0l-4-4m4 4l-4 4"/></svg>
                    Email
                  </a>
                </div>
                <div class="text-gray-600 dark:text-gray-400 text-base">I'll get back to you as soon as possible!</div>
            </div>
          </div>
        </section>
    </main>
    <SectionNavArrows />
</template>

<style scoped>
html {
  scroll-behavior: smooth;
}
</style> 