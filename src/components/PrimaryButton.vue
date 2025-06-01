<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    tag: {
        type: String,
        default: 'button',
    },
    href: {
        type: String,
        default: '',
    },
});
</script>

<template>
    <component
        :is="props.tag === 'a' ? 'a' : 'button'"
        v-bind="props.tag === 'a' ? { href: props.href, target: '_blank', rel: 'noopener noreferrer' } : {}"
        class="inline-flex items-center rounded-md border border-transparent bg-gray-800 dark:bg-gray-100 px-4 py-2 text-xs font-semibold uppercase tracking-widest text-white dark:text-gray-900 transition duration-150 ease-in-out hover:bg-gray-700 dark:hover:bg-white focus:bg-gray-700 dark:focus:bg-white focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 active:bg-gray-900 dark:active:bg-gray-200"
    >
        <slot />
    </component>
</template>
