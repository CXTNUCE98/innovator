<script setup lang="ts">

const router= useRouter()
function handleRedirect(id: string) {
    router.push(`/teamofexperts/${id}`)
}
</script>
<template>
    <!-- Banner Section with improved responsiveness -->
    <SharedHeaderPage title="Đội ngũ chuyên gia"
        subTitle="Đội ngũ chuyên gia của Innovator Academy  cam kết mang đến những chương trình đào tạo chất lượng và hiệu quả nhất, giúp các doanh nghiệp phát triển bền vững và đạt được thành công lâu dài." />

    <!-- Main Content -->
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-12 md:py-16 lg:py-20">
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 md:gap-8">
            <div v-for="(item, index) in teamOfExperts" :key="index"
            @click="handleRedirect(item.id)"
                class="profile-card rounded-lg overflow-hidden transform transition-all cursor-pointer duration-300">
                <div class="aspect-square overflow-hidden relative group">
                    <img :src="item.img" :alt="item.name"
                        class="w-full h-full rounded-lg object-cover transition-transform duration-500 " />
                </div>
                <div class="text-center py-4">
                    <div class="text-20px text-#FCAF17 font-bold">{{ item.name }}</div>
                    <div class="text-16px text-#555555">{{ item.duty }}</div>
                </div>
            </div>
        </div>
    </div>
</template>
<style scoped>
@keyframes fadeIn {
    from {
        opacity: 0;
        transform: translateY(20px);
    }

    to {
        opacity: 1;
        transform: translateY(0);
    }
}

@keyframes slideInTop {
    from {
        opacity: 0;
        transform: translateY(-30px);
    }

    to {
        opacity: 1;
        transform: translateY(0);
    }
}

@keyframes pulse {
    0% {
        transform: scale(1);
    }

    50% {
        transform: scale(1.05);
    }

    100% {
        transform: scale(1);
    }
}

.animate-fadeIn {
    animation: fadeIn 0.5s ease-out forwards;
}

.slide-in-top {
    animation: slideInTop 0.8s ease-out forwards;
}

.profile-card {
    transition: all 0.3s ease;
}



/* For dark mode support */
@media (prefers-color-scheme: dark) {
    .profile-card {
        background-color: #1f2937;
    }

    .profile-card h3 {
        color: #fbbf24;
    }

    .profile-card p {
        color: #9ca3af;
    }
}

/* Media query for responsive adjustments */
@media (max-width: 640px) {
    .profile-card {
        margin-bottom: 1.5rem;
    }
}
</style>