<script setup lang="ts">
import Banner from "@/public/banner_introduce.png"

const props = defineProps<{
    title: string
    subTitle: boolean
}>()

</script>

<template>
    <div class="relative flex justify-center items-center py-16 md:py-24 lg:py-29 overflow-hidden">
        <img class="absolute w-full h-full md:h-auto object-cover" :src="Banner"
            alt="banner-introduce">
        <div class="absolute inset-0 "></div>
        <div class="relative z-10 w-full max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 ">
            <div class="flex flex-col md:flex-row gap-6 md:gap-12 mt-10 md:mt-0">
                <div class="w-full md:w-1/2">
                    <h1 class="text-2xl sm:text-3xl lg:text-4xl font-bold text-#2A2A2A mb-0 md:mb-4">{{title}}</h1>
                </div>
                <div class="w-full md:w-1/2">
                    <p class="text-base sm:text-lg lg:text-xl text-#555555 opacity-90">
                        {{subTitle}}
                    </p>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
@media (prefers-reduced-motion: reduce) {
    .animate-on-scroll {
        opacity: 1 !important;
        transform: translateY(0) !important;
        transition: none !important;
    }
}

.delay-100 {
    transition-delay: 0.1s;
}

.playfair-display {
    font-family: 'Playfair Display', serif;
    font-optical-sizing: auto;
    font-weight: 500;
}
</style>