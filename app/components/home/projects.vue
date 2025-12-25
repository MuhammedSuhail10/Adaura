<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const emit = defineEmits(['enter']);
const sectionRef = ref(null);
let observer = null;

onMounted(() => {
    observer = new IntersectionObserver(
        ([entry]) => {
            if (entry.isIntersecting) {
                emit('enter');
            }
        },
        { threshold: 0.3 }
    );

    if (sectionRef.value) {
        observer.observe(sectionRef.value);
    }
});

onUnmounted(() => {
    if (observer && sectionRef.value) {
        observer.unobserve(sectionRef.value);
    }
});
</script>

<template>
    <div ref="sectionRef" class="xl:px-[10em] lg:px-[5em] px-[1em] py-[3em]">
        <h2 class="text-center lg:text-[35pt] text-[25pt] lg:px-[5em] font-bold">
            Projects
        </h2>
        <div class="flex lg:flex-row flex-col lg:gap-[1em] gap-[0.5em] my-[2em]">
            <div class="lg:w-[65%] flex flex-col lg:gap-[1em] gap-[0.5em]">
                <div class="h-[25em] rounded-[3em] bg-[#9C9C9C]"></div>
                <div class="flex lg:gap-[1em] gap-[0.5em]">
                    <div class="lg:h-[25em] h-[15em] w-[50%] rounded-[3em] bg-[#9C9C9C]"></div>
                    <div class="lg:h-[25em] h-[15em] w-[50%] rounded-[3em] bg-[#9C9C9C]"></div>
                </div>
            </div>
            <div class="lg:w-[35%] w-[100%] gap-[1em]">
                <div class="h-[100%] w-[100%] rounded-[3em] bg-[#9C9C9C]"></div>
            </div>
        </div>
        <div class="flex justify-center">
            <div class="lg:w-[250px] ">
                <div class="flex gap-[0.1em] items-center group relative">
                    <button
                        class="group-hover:bg-[#669bbc] border-1 border-[#669bbc] text-[#669bbc] group-hover:text-white px-[5em] py-[1.5em] rounded-full font-semibold transition-all duration-300 ease-in-out whitespace-nowrap">
                        All Projects
                    </button>
                    <button
                        class="group-hover:bg-[#669bbc] border-1 border-[#669bbc] text-[#669bbc] group-hover:text-white px-[1.5em] group-hover:px-[1.5em] py-[1.5em] rounded-full group-hover:rounded-l-[0] font-semibold transition-all duration-300 ease-in-out relative z-10 group-hover:-ml-[5em] absolute right-0">
                        <svg xmlns="http://www.w3.org/2000/svg" height="24px"
                            class="transition-transform duration-300 ease-in-out rotate-[-45deg] group-hover:rotate-[0deg]"
                            viewBox="0 -960 960 960" width="24px" fill="currentColor">
                            <path d="m560-240-56-58 142-142H160v-80h486L504-662l56-58 240 240-240 240Z" />
                        </svg>
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>