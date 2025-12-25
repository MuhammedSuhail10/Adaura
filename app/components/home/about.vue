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
    <div ref="sectionRef" class="xl:px-[10em] lg:px-[5em] px-[1em]">
        <h2 class="text-center lg:text-[35pt] text-[25pt] xl:px-[5em] lg:px-[2em] font-bold">
            A <span class="italic font-extralight">custom-built strategy</span> for a one-of-a-kind brand
        </h2>
        <div class="flex flex-col lg:flex-row my-[1em]">
            <p class="xl:text-[18pt] lg:text-[15pt] text-[13pt] lg:w-[65%] xl:w-[70%] lg:border-r-[0.5px] border-black/40 lg:pr-[2em]">
                We don't believe in cookie-cutter templates because we understand that your business is a distinct
                entity with its own set of hurdles, goals, and market dynamics. A generic, "one-size-fits-all" approach
                rarely addresses the specific friction points that hold a company back from its true potential; instead,
                we believe your digital strategy should be a bespoke reflection of your brand's unique DNA.

                Our process is built on deep immersion and strategic precision: starting with a comprehensive audit of
                your current ecosystem, we identify hidden opportunities and eliminate inefficiencies. From that initial
                discovery through to meticulous execution, we provide a customized, end-to-end roadmap designed to
                outpace the competition and secure your digital dominance. We don't just offer services; we build the
                technical and creative infrastructure necessary for you to lead your industry.
            </p>
            <div class="flex text-[20pt] lg:w-[25%] text-center lg:pl-[2em] lg:flex-col justify-center my-[1em] gap-[1em]">
                <p class="border-r-1 lg:border-r-0  border-black/40 pr-[1em]"><strong>5 Year</strong> <br>Experience</p>
                <p><strong>10+</strong> Happy <br>Clients</p>
            </div>
        </div>
    </div>
</template>