<script setup lang="ts">
useSeoMeta({
    title: 'Adaura Advertising Agency',
    ogTitle: 'Adaura Advertising Agency',
    description:
        'Adaura Advertising Agency provides innovative marketing solutions, creative design, and strategic branding services to help businesses grow and succeed in a competitive market.',
    ogDescription:
        'Adaura Advertising Agency provides innovative marketing solutions, creative design, and strategic branding services to help businesses grow and succeed in a competitive market.',
    ogImage: '/favicon.ico',
})
import { ref } from 'vue';

const pageBackground = ref('bg-black');

const handleBackgroundChange = (color: string) => {
  pageBackground.value = color;
};
</script>

<template>
    <div :class="['font-[elms] transition-colors duration-700', pageBackground]">
        <LinksNav />
        <HomeHero @enter="handleBackgroundChange('bg-black')" />
        <div class="xl:mt-[70vh] lg:mt-[65vh] mt-[25vh]">
            <LazyHomeAbout @enter="handleBackgroundChange('bg-[#f8f8f8]')" />
        </div>
        <LazyHomeProjects @enter="handleBackgroundChange('bg-[#f8f8f8]')" />
        <LazyHomeProcedure @enter="handleBackgroundChange('bg-[#f8f8f8]')" />
        <LazyLinksFooter @enter="handleBackgroundChange('bg-black')" />
    </div>
</template>