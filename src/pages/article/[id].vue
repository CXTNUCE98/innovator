<script setup lang="ts">
const route = useRoute()
const idBlog = computed(() => {
    return route?.params?.id as string
})

const blockDetail = ref(articles.value?.find((el) => el.id === idBlog.value))
</script>

<template>
    <div class="max-w-6xl mx-auto mt-64px px-4 py-8 md:py-12">
        <div class="hidden md:block pb-32px">
            <i class='bx bx-arrow-back rounded-full bg-#F5F5F5 p-2 text-20px '></i>
        </div>

        <img :src="blockDetail?.image" alt="Dropshipping Success"
            class="rounded-lg h-400px shadow-lg object-cover w-full" />

        <section class="relative overflow-hidden rounded-lg">
            <div class="flex flex-col md:flex-row items-center">
                <div class="">
                    <h1 class="text-28px md:text-32px font-bold pt-64px pb-40px  animate-fadeIn">
                        {{ blockDetail?.title }}
                    </h1>
                    <p class="text-20px text-gray-600 mb-6 animate-slideUp">
                        {{ blockDetail?.des }}
                    </p>
                </div>
            </div>
        </section>

        <!-- Main Content Section -->
        <section class="bg-white rounded-lg mb-6 animate-fadeIn">
            <h2 class="text-20px font-bold text-gray-800 mb-6">{{ blockDetail?.subTitle }}</h2>

            <div class="space-y-6">
                <div class="animate-slideRight" style="animation-delay: 0.2s">
                    <div v-for=" (item, index) in blockDetail?.benefits?.benefit">
                        <p class="text-gray-600 text-20px">{{ index + 1 }}. {{ item }}</p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Strategy Section -->
        <section class="rounded-lg mb-12 animate-fadeIn">
            <h2 class="text-20px font-bold text-gray-800  mb-6">{{ blockDetail?.benefits?.content }}</h2>

            <div class="space-y-6">
                <div class="animate-slideRight" style="animation-delay: 0.2s">
                    <div v-for=" (item, index) in blockDetail?.benefits?.benefit2">
                        <p class="text-gray-600 text-20px">{{ index + 1 }}. {{ item }}</p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Related Articles Section -->
        <section class="mb-6 animate-fadeIn">
            <BlogCarousel />            
        </section>

    </div>
</template>

<style scoped>
/* Animations */
.animate-fadeIn {
    animation: fadeIn 1s ease-out;
}

.animate-slideUp {
    animation: slideUp 0.8s ease-out;
}

.animate-slideRight {
    animation: slideRight 0.8s ease-out;
}

.animate-slideLeft {
    animation: slideLeft 0.8s ease-out;
}

.animate-floatUp {
    animation: floatUp 3s ease-in-out infinite;
}

@keyframes fadeIn {
    from {
        opacity: 0;
    }

    to {
        opacity: 1;
    }
}

@keyframes slideUp {
    from {
        opacity: 0;
        transform: translateY(20px);
    }

    to {
        opacity: 1;
        transform: translateY(0);
    }
}

@keyframes slideRight {
    from {
        opacity: 0;
        transform: translateX(-20px);
    }

    to {
        opacity: 1;
        transform: translateX(0);
    }
}

@keyframes slideLeft {
    from {
        opacity: 0;
        transform: translateX(20px);
    }

    to {
        opacity: 1;
        transform: translateX(0);
    }
}

@keyframes floatUp {

    0%,
    100% {
        transform: translateY(0);
    }

    50% {
        transform: translateY(-10px);
    }
}

/* Responsive adjustments */
@media (max-width: 768px) {
    .container {
        padding-left: 16px;
        padding-right: 16px;
    }
}

<style>

/* Animations */
.animate-fadeIn {
    animation: fadeIn 1s ease-out;
}

.animate-slideUp {
    animation: slideUp 0.8s ease-out;
}

.animate-slideRight {
    animation: slideRight 0.8s ease-out;
}

.animate-slideLeft {
    animation: slideLeft 0.8s ease-out;
}

.animate-floatUp {
    animation: floatUp 3s ease-in-out infinite;
}

@keyframes fadeIn {
    from {
        opacity: 0;
    }

    to {
        opacity: 1;
    }
}

@keyframes slideUp {
    from {
        opacity: 0;
        transform: translateY(20px);
    }

    to {
        opacity: 1;
        transform: translateY(0);
    }
}

@keyframes slideRight {
    from {
        opacity: 0;
        transform: translateX(-20px);
    }

    to {
        opacity: 1;
        transform: translateX(0);
    }
}

@keyframes slideLeft {
    from {
        opacity: 0;
        transform: translateX(20px);
    }

    to {
        opacity: 1;
        transform: translateX(0);
    }
}

@keyframes floatUp {

    0%,
    100% {
        transform: translateY(0);
    }

    50% {
        transform: translateY(-10px);
    }
}

/* Responsive adjustments */
@media (max-width: 768px) {
    .container {
        padding-left: 16px;
        padding-right: 16px;
    }
}
</style>