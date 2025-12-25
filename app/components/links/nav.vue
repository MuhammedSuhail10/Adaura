<template>
    <div class="xl:px-[10em] lg:px-[5em] px-[1em] h-[10vh] bg-[#000] sticky z-50  flex justify-between items-center"
        :class="isScrolled ? 'bg-[#F8F8F8] top-0 shadow-sm transition-colors duration-300' : ''">
        <div>
            <img src="~/assets/images/icon.png" alt="" width="150">
        </div>
        <div class="lg:hidden flex items-center">
            <button class="hover:fill-[#669bbc]" :class="isScrolled ? 'text-[#000]' : 'text-[#f8f8f8]'"
                @click="isMenuOpen = true" aria-label="Open menu">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 -960 960 960" height="25px" width="25px"
                    fill="currentcolor">
                    <path d="M120-240v-80h720v80H120Zm0-200v-80h720v80H120Zm0-200v-80h720v80H120Z" />
                </svg>
            </button>
        </div>
        <div class="hidden lg:block">
            <nav class="hidden lg:flex gap-10 text-[13pt] font-semibold"
                :class="isScrolled ? 'text-black/60 ' : 'text-white/60'">
                <NuxtLink class="hover:text-[#669bbc] text-[1.2em]" active-class="text-[#669bbc] font-semibold" exact
                    to="/">Home</NuxtLink>
                <NuxtLink class="hover:text-[#669bbc] text-[1.2em]" active-class="text-[#669bbc] font-semibold" exact
                    to="/about">About</NuxtLink>
                <NuxtLink class="hover:text-[#669bbc] text-[1.2em]" active-class="text-[#669bbc] font-semibold" exact
                    to="/projects">Projects</NuxtLink>
                <NuxtLink class="hover:text-[#669bbc] text-[1.2em]" active-class="text-[#669bbc] font-semibold" exact
                    to="/contact">Contact</NuxtLink>
            </nav>
        </div>
        <div class="w-[250px] lg:block hidden">
            <div class="flex gap-[0.1em] items-center group relative">
                <button
                    class="group-hover:bg-[#669bbc] border-1 border-[#669bbc] text-[#669bbc] group-hover:text-white px-[3em] py-[1em] rounded-full group-hover:rounded-r-[0] font-semibold transition-all duration-300 ease-in-out whitespace-nowrap">
                    Let's Connect
                </button>
                <button
                    class="group-hover:bg-[#669bbc] border-1 border-[#669bbc] text-[#669bbc] group-hover:text-white px-[1em] group-hover:px-[1.5em] py-[1em] rounded-full group-hover:rounded-l-[0] font-semibold transition-all duration-300 ease-in-out relative z-10 group-hover:-ml-[3em] absolute right-0">
                    <svg xmlns="http://www.w3.org/2000/svg" height="24px"
                        class="transition-transform duration-300 ease-in-out rotate-[-45deg] group-hover:rotate-[0deg]"
                        viewBox="0 -960 960 960" width="24px" fill="currentColor">
                        <path d="m560-240-56-58 142-142H160v-80h486L504-662l56-58 240 240-240 240Z" />
                    </svg>
                </button>
            </div>
        </div>
    </div>

    <ClientOnly>
        <HelpersDrawer v-if="isMenuOpen" :class="isAbout ? 'bg-[#F0F8FF]' : 'bg-[#0f0f0f]'" :is-menu-open="isMenuOpen"
            @close="isMenuOpen = false" />
    </ClientOnly>
</template>

<script setup>
import { ref, onMounted, onUnmounted, watch } from 'vue'

const isScrolled = ref(false)

const handleScroll = () => {
    isScrolled.value = window.scrollY > 50
}

onMounted(() => {
    window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
    window.removeEventListener('scroll', handleScroll)
    // Cleanup: ensure scroll is restored
    document.body.style.overflow = ''
})

const route = useRoute()
const isMenuOpen = ref(false)

// Close drawer on route change
watch(
    () => route.path,
    () => {
        isMenuOpen.value = false
    }
)

// Lock/unlock body scroll when drawer opens/closes
watch(isMenuOpen, (newValue) => {
    if (newValue) {
        document.body.style.overflow = 'hidden'
    } else {
        document.body.style.overflow = ''
    }
})
</script>