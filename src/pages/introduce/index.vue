<script setup lang="ts">
// Reactive data for team members
const teammembers = ref([
    {
        id: 1,
        name: 'Mr. Trần Quốc Lợi',
        position: 'Cố đồng sáng lập'
    },
    {
        id: 2,
        name: 'Mr. Trần Quốc Lợi',
        position: 'Cố đồng sáng lập'
    },
    {
        id: 3,
        name: 'Mr. Trần Quốc Lợi',
        position: 'Cố đồng sáng lập'
    },
    {
        id: 4,
        name: 'Mr. Trần Quốc Lợi',
        position: 'Cố đồng sáng lập'
    }
]);

// Stats data
const stats = ref([
    { value: '10K+', label: 'Học viên' },
    { value: '75%', label: 'Bán hàng Dropship' },
    { value: '25%', label: 'Bán hàng Amazon' },
    { value: '10%', label: 'Học viên đạt doanh thu >10000$' },
    { value: '55%', label: 'Học viên đạt doanh thu >3000$' }
]);

// Intersection observer for animations
onMounted(() => {
    const sections = document.querySelectorAll('.animate-section');

    const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.classList.add('visible');
            }
        });
    }, { threshold: 0.1 });

    sections.forEach(section => {
        observer.observe(section);
    });
});
</script>

<template>
    <!-- Banner Section with improved responsiveness -->
    <div class="relative flex justify-center items-center py-16 md:py-24 lg:py-32 overflow-hidden">
        <img class="absolute w-full h-full md:h-auto object-cover" src="../../public/banner_introduce.png" alt="banner-introduce">
        <div class="absolute inset-0 "></div>
        <div class="relative z-10 w-full max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex flex-col md:flex-row gap-6 md:gap-12">
                <div class="w-full md:w-1/2">
                    <h1 class="text-2xl sm:text-3xl lg:text-4xl font-bold text-#2A2A2A mb-4">Về chúng tôi</h1>
                </div>
                <div class="w-full md:w-1/2">
                    <p class="text-base sm:text-lg lg:text-xl text-#555555 opacity-90">
                        Chúng tôi quyết tâm trở thành một trung tâm đào tạo hàng đầu, là nguồn lực đáng tin cậy cho sự phát
                        triển
                        nhân lực ưu tú, có khả năng thích ứng linh hoạt với công nghệ 4.0 và đóng góp tích cực vào sự phát
                        triển bền
                        vững của cộng đồng và xã hội.
                    </p>
                </div>
            </div>
        </div>
    </div>

    <!-- Main Content -->
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-12 md:py-16 lg:py-20">
        <!-- Mission Section -->
        <section class="mb-16 md:mb-24 animate-section">
            <h2 class="text-2xl md:text-3xl font-bold text-center mb-8 md:mb-16">TẦM NHÌN - SỨ MỆNH - MỤC TIÊU</h2>

            <div class="grid grid-cols-1 md:grid-cols-3 gap-8 md:gap-6">
                <!-- Mission Card 1 -->
                <div
                    class="p-5 md:p-6 rounded-lg shadow-md relative transition duration-300 animate-item min-h-[250px] flex flex-col">
                    <div
                        class="absolute -top-5 left-1/2 transform -translate-x-1/2 w-10 h-10 rounded-full  shadow-md flex items-center justify-center">
                        <div class="w-8 h-8 rounded-full bg-yellow-400 flex items-center justify-center">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-white" fill="none"
                                viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                    d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                    d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
                            </svg>
                        </div>
                    </div>
                    <div class="mt-6">
                        <p class="text-gray-600 text-sm sm:text-base">
                            Chúng tôi quyết tâm trở thành một trung tâm đào tạo hàng đầu, là nguồn tác động tích cực đến sự
                            phát triển năng lực và tư duy kinh doanh của thế hệ trẻ Việt Nam, và đồng góp vào sự phát triển
                            bền vững của cộng đồng và xã hội.
                        </p>
                    </div>
                </div>

                <!-- Mission Card 2 -->
                <div
                    class="bg-white p-5 md:p-6 rounded-lg shadow-md relative transition duration-300 animate-item delay-100 min-h-[250px] flex flex-col">
                    <div
                        class="absolute -top-5 left-1/2 transform -translate-x-1/2 w-10 h-10 rounded-full bg-white shadow-md flex items-center justify-center">
                        <div class="w-8 h-8 rounded-full bg-green-400 flex items-center justify-center">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-white" fill="none"
                                viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                    d="M12 11c0 3.517-1.009 6.799-2.753 9.571m-3.44-2.04l.054-.09A13.916 13.916 0 008 11a4 4 0 118 0c0 1.017-.07 2.019-.203 3m-2.118 6.844A21.88 21.88 0 0015.171 17m3.839 1.132c.645-2.266.99-4.659.99-7.132A8 8 0 008 4.07M3 15.364c.64-1.319 1-2.8 1-4.364 0-1.457.39-2.823 1.07-4" />
                            </svg>
                        </div>
                    </div>
                    <div class="mt-6">
                        <p class="text-gray-600 text-sm sm:text-base">
                            Với niềm đam mê về sự sáng tạo và sứ mệnh giáo dục, chúng tôi cam kết cung cấp những trải nghiệm
                            học tập chất lượng cao, sáng tạo và hiệu quả. Chúng tôi cam kết đồng hành trên con đường phát
                            triển của học viên, từ đào tạo đến tự triển khai thực tiễn.
                        </p>
                    </div>
                </div>

                <!-- Mission Card 3 -->
                <div
                    class="bg-white p-5 md:p-6 rounded-lg shadow-md relative transition duration-300 animate-item delay-200 min-h-[250px] flex flex-col">
                    <div
                        class="absolute -top-5 left-1/2 transform -translate-x-1/2 w-10 h-10 rounded-full bg-white shadow-md flex items-center justify-center">
                        <div class="w-8 h-8 rounded-full bg-blue-300 flex items-center justify-center">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-white" fill="none"
                                viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                    d="M13 10V3L4 14h7v7l9-11h-7z" />
                            </svg>
                        </div>
                    </div>
                    <div class="mt-6">
                        <p class="text-gray-600 text-sm sm:text-base">
                            Chúng tôi dành tầm tuyệt đối tạo ra một môi trường đào tạo chất lượng cao, nơi kết hợp giữa công
                            nghệ 4.0 và giáo trình thực tiễn. Sự sáng tạo và đổi mới là điều cốt lõi trong tầm nhìn và được
                            thực hiện thông qua trực tiếp đào tạo và đồng hành triển khai thực tiễn từ các chuyên gia kinh
                            doanh cá nhân & doanh nghiệp.
                        </p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Achievement Section -->
        <section class="mb-16 md:mb-24 animate-section">
            <h2 class="text-2xl md:text-3xl font-bold text-center mb-4">THÀNH TÍCH</h2>
            <p class="text-center text-gray-600 mb-8 md:mb-12 max-w-3xl mx-auto">
                Innovator Academy chính thức trở thành đơn vị đào tạo đầu tiên tại Việt Nam được kiểm định và cấp
                <span class="text-yellow-500 font-bold">Chứng nhận đào tạo</span> về Thương mại điện tử từ cơ quan quản lý
                nhà nước.
            </p>

            <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-4 md:gap-6">
                <div v-for="(stat, index) in stats" :key="index"
                    class="text-center p-4 transition duration-300 hover:scale-105 animate-item "
                    :class="`delay-${index * 100}`">
                    <div class="text-2xl md:text-3xl font-bold text-yellow-500">{{ stat.value }}</div>
                    <div class="text-gray-600 text-sm md:text-base mt-2">{{ stat.label }}</div>
                </div>
            </div>
        </section>

        <!-- Team Section -->
        <section class="animate-section">
            <h2 class="text-2xl md:text-3xl font-bold text-center mb-4">BAN ĐIỀU HÀNH</h2>
            <p class="text-center text-gray-600 mb-8 md:mb-12 max-w-3xl mx-auto">
                Với đội ngũ lãnh đạo tài năng và tầm huyết, Innovator Academy luôn sẵn sàng đồng hành cùng khách hàng trên
                con đường chinh phục thành công.
            </p>

            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6 md:gap-8">
                <div v-for="(member, index) in teammembers" :key="member.id"
                    class="transition duration-300 hover:-translate-y-1 animate-item group" :class="`delay-${index * 100}`">
                    <div
                        class="bg-gray-200 rounded-lg aspect-square mb-4 overflow-hidden group-hover:shadow-lg transition-shadow duration-300">
                    </div>
                    <h3 class="text-center font-medium text-yellow-500 text-lg">{{ member.name }}</h3>
                    <p class="text-center text-gray-600 text-sm">{{ member.position }}</p>
                </div>
            </div>
        </section>
    </div>
</template>
<style scoped>
/* Custom animations that can't be done with Tailwind alone */
.animate-section {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.8s ease, transform 0.8s ease;
}

.animate-section.visible {
    opacity: 1;
    transform: translateY(0);
}

.animate-item {
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.5s ease, transform 0.5s ease;
}

.animate-section.visible .animate-item {
    opacity: 1;
    transform: translateY(0);
}

.delay-0 {
    transition-delay: 0.1s;
}

.delay-100 {
    transition-delay: 0.2s;
}

.delay-200 {
    transition-delay: 0.3s;
}

.delay-300 {
    transition-delay: 0.4s;
}

.delay-400 {
    transition-delay: 0.5s;
}

/* Additional media queries for finer responsive control */
@media (max-width: 640px) {
    .mission-card {
        min-height: 200px;
    }
}

@media (min-width: 1024px) {
    .mission-card {
        min-height: 230px;
    }
}
</style>