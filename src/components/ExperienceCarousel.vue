<script setup>
import { ref } from 'vue';

const experiences = [
  {
    title: 'Full Stack Developer',
    company: 'TheGameCreators Ltd',
    years: 'Sep 2023 – present',
    logo: '/images/thegamecreators-logo.png',
    icon: 'code', // Placeholder, use SVG below
    description: 'Building and maintaining the Driving Theory Test 4 in 1 Kit, the UK\'s No. 1 Paid iOS/Android app, focusing on backend and frontend development.',
    tags: ['Laravel', 'Vue', 'React Native', 'PHP', 'MySQL', 'API Development', 'UI/UX', 'Team Collaboration'],
    bullets: [
      'Upgraded the application from an in-house C++ language to React Native.',
      'Developed API endpoints, managed table migrations, and created scheduled commands.',
      'Enhanced the admin management site for user management and analytics.',
      'Implemented new features: video messaging, onboarding signup flow, main menu screens, leaderboards, Halloween update.',
      'Collaborated closely with a small development team to deliver new functionalities and improvements.'
    ]
  },
  {
    title: 'Front-End Web Developer',
    company: 'Manchester Metropolitan University',
    years: 'May 2023 – July 2023',
    logo: '/images/man-met-crest.png',
    icon: 'university',
    description: 'Developed a gaming social media mobile app MVP as part of a small team.',
    tags: ['React Native', 'Firebase', 'Steam API', 'YouTube API', 'UI/UX', 'Teamwork'],
    bullets: [
      'Built a gaming social media mobile app MVP using React Native and Firebase.',
      'Integrated Steam and YouTube APIs for authentication and data.',
      'Developed front-end and back-end integration for user features.',
      'Collaborated on UI/UX based on client specifications and wireframes.'
    ]
  },
  {
    title: 'IT & Data Administration Roles',
    company: 'Learning Links Europe Ltd, Manchester Royal Infirmary',
    years: '2013–2019',
    icon: 'briefcase',
    description: 'Developed strong foundations in IT support, data management, and team collaboration across multiple roles in education and healthcare.',
    tags: ['IT Support', 'Data Management', 'Reporting', 'Teamwork', 'Mentoring', 'Troubleshooting', 'Communication'],
    bullets: [
      'Managed and operated learner management systems, producing regular reports and statistics.',
      'Assisted with diagnosing and troubleshooting IT issues in office and healthcare settings.',
      'Supervised new apprentices and distributed tasks to support their development.',
      'Promoted to secondment roles, working with management during audit periods.',
      'Developed strong communication, organizational, and process improvement skills.'
    ]
  }
];

const current = ref(0);

function prev() {
  current.value = (current.value - 1 + experiences.length) % experiences.length;
}
function next() {
  current.value = (current.value + 1) % experiences.length;
}
</script>

<template>
  <div class="relative w-full max-w-3xl mx-auto">
    <div class="flex items-center justify-center">
      <button @click="prev" class="hidden md:block p-2 rounded-full bg-gray-100 dark:bg-gray-800 hover:bg-blue-100 dark:hover:bg-blue-900 shadow transition mr-2" aria-label="Previous">
        <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7" /></svg>
      </button>
      <div class="overflow-hidden w-full">
        <div class="flex transition-transform duration-500" :style="{ transform: `translateX(-${current * 100}%)` }">
          <div v-for="(exp, i) in experiences" :key="i" class="w-full flex-shrink-0">
            <div class="bg-white dark:bg-gray-800 rounded-2xl shadow-xl p-8 flex flex-col gap-4 h-full border border-gray-200 dark:border-gray-700">
              <!-- Icon/Logo -->
              <div class="flex items-center gap-3 mb-2">
                <div class="p-3 rounded-full bg-gray-100 dark:bg-gray-700 flex items-center justify-center w-14 h-14">
                  <img v-if="exp.logo" :src="exp.logo" :alt="exp.company + ' logo'" class="max-h-8 max-w-24 object-contain dark:invert" />
                  <template v-else>
                    <svg v-if="exp.icon === 'briefcase'" class="w-7 h-7 text-blue-600 dark:text-blue-300" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" d="M4 7V6a2 2 0 012-2h12a2 2 0 012 2v1"/>
                      <path stroke-linecap="round" stroke-linejoin="round" d="M2 7h20v13a2 2 0 01-2 2H4a2 2 0 01-2-2V7z"/>
                      <path stroke-linecap="round" stroke-linejoin="round" d="M16 21v-4a2 2 0 00-2-2H10a2 2 0 00-2 2v4"/>
                    </svg>
                    <svg v-else-if="exp.icon === 'university'" class="w-7 h-7 text-green-600 dark:text-green-300" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M12 14l9-5-9-5-9 5 9 5z"/><path stroke-linecap="round" stroke-linejoin="round" d="M12 14l6.16-3.422A12.083 12.083 0 0121 13.5c0 2.485-4.03 4.5-9 4.5s-9-2.015-9-4.5c0-.538.214-1.05.84-1.922L12 14z"/></svg>
                    <svg v-else class="w-7 h-7 text-purple-600 dark:text-purple-300" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M16 18l6-6-6-6"/><path stroke-linecap="round" stroke-linejoin="round" d="M8 6l-6 6 6 6"/></svg>
                  </template>
                </div>
                <div class="flex flex-col items-start">
                  <div class="text-lg font-bold">{{ exp.title }}</div>
                  <div class="text-sm text-gray-600 dark:text-gray-400">{{ exp.company }}</div>
                </div>
                <div class="ml-auto text-sm font-semibold text-gray-500 dark:text-gray-400">{{ exp.years }}</div>
              </div>
              <div class="text-base text-gray-700 dark:text-gray-200 mb-2">{{ exp.description }}</div>
              <!-- Tags -->
              <div class="flex flex-wrap gap-2 mb-2">
                <span v-for="tag in exp.tags" :key="tag" class="px-3 py-1 rounded-full text-xs font-semibold bg-gray-100 dark:bg-gray-700 text-gray-700 dark:text-gray-200">{{ tag }}</span>
              </div>
              <!-- Bullets -->
              <ul class="list-disc list-inside text-left text-gray-700 dark:text-gray-200 pl-2 space-y-1">
                <li v-for="b in exp.bullets" :key="b">{{ b }}</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
      <button @click="next" class="hidden md:block p-2 rounded-full bg-gray-100 dark:bg-gray-800 hover:bg-blue-100 dark:hover:bg-blue-900 shadow transition ml-2" aria-label="Next">
        <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9 5l7 7-7 7" /></svg>
      </button>
    </div>
    <!-- Mobile arrows -->
    <div class="flex justify-between mt-4 md:hidden">
      <button @click="prev" class="p-2 rounded-full bg-gray-100 dark:bg-gray-800 hover:bg-blue-100 dark:hover:bg-blue-900 shadow transition" aria-label="Previous">
        <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7" /></svg>
      </button>
      <button @click="next" class="p-2 rounded-full bg-gray-100 dark:bg-gray-800 hover:bg-blue-100 dark:hover:bg-blue-900 shadow transition" aria-label="Next">
        <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9 5l7 7-7 7" /></svg>
      </button>
    </div>
  </div>
</template>

<style scoped>
/**** Hide scrollbar for carousel ****/
::-webkit-scrollbar {
  display: none;
}
</style> 