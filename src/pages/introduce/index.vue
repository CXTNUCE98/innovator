<script setup lang="ts">
import Moment1 from "@/public/moment-1.png"
import Moment2 from "@/public/moment-2.png"
import Moment3 from "@/public/moment-3.png"
import Moment4 from "@/public/moment-4.png"
import Moment5 from "@/public/moment-5.png"
import Moment6 from "@/public/moment-6.png"

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
    { value: 10, label: 'Học viên', unit: 'K+', current: 0 },
    { value: 75, label: 'Bán hàng Dropship', unit: '%', current: 0 },
    { value: 25, label: 'Bán hàng Amazon', unit: '%', current: 0 },
    { value: 10, label: 'Học viên đạt doanh thu >10000$', unit: '%', current: 0 },
    { value: 55, label: 'Học viên đạt doanh thu >3000$', unit: '%', current: 0 }
]);

// Function to animate counting
function animateValue(item, duration = 1500) {
    const startValue = 0;
    const endValue = item.value;
    const startTime = performance.now();

    const updateValue = (currentTime) => {
        const elapsedTime = currentTime - startTime;
        const progress = Math.min(elapsedTime / duration, 1);

        // Easing function for smoother animation (ease-out)
        const easeOutProgress = 1 - Math.pow(1 - progress, 3);

        item.current = Math.floor(startValue + (endValue - startValue) * easeOutProgress);

        if (progress < 1) {
            requestAnimationFrame(updateValue);
        } else {
            item.current = endValue; // Ensure we end at the exact target value
        }
    };

    requestAnimationFrame(updateValue);
}

// Flag to track if stats animation has run
const statsAnimated = ref(false);

// Intersection observer for animations
onMounted(() => {
    const sections = document.querySelectorAll('.animate-section');
    const statsSection = document.querySelector('.stats-section');

    const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.classList.add('visible');

                // Start stats animation when stats section becomes visible (only once)
                if (entry.target.classList.contains('stats-section') && !statsAnimated.value) {
                    statsAnimated.value = true; // Set flag to true so animation only runs once
                    stats.value.forEach((stat, index) => {
                        // Stagger the animations slightly
                        setTimeout(() => {
                            animateValue(stat, 2000);
                        }, index * 150);
                    });
                }
            }
        });
    }, { threshold: 0.15 });

    sections.forEach(section => {
        observer.observe(section);
    });
});

const images = ref([
    {
        id: 1,
        src: Moment1,
        alt: 'Academy team members',
    },
    {
        id: 2,
        src: Moment2,
        alt: 'Training session',
    },
    {
        id: 3,
        src: Moment3,
        alt: 'Celebration event',
    },
    {
        id: 4,
        src: Moment4,
        alt: 'Vietnam brand celebration',
    },
    {
        id: 5,
        src: Moment5,
        alt: 'Award ceremony',
    },
    {
        id: 6,
        src: Moment6,
        alt: 'Team meeting',
    },
]);
</script>

<template>
    <!-- Banner Section with improved responsiveness -->
    <SharedHeaderPage title="Về chúng tôi" subTitle="Chúng tôi quyết tâm trở thành một trung tâm đào tạo hàng đầu, là nguồn lực đáng tin cậy cho sự phát
                        triển
                        nhân lực ưu tú, có khả năng thích ứng linh hoạt với công nghệ 4.0 và đóng góp tích cực vào sự phát
                        triển bền
                        vững của cộng đồng và xã hội." />

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
                        class="absolute -top-5 left-1/2 transform -translate-x-1/2 w-14 h-14 rounded-full bg-#FFFBF1 shadow-md flex items-center justify-center">
                        <div class="w-8 h-8 rounded-full  flex items-center justify-center">
                            <img src="@/public/eye.png" alt="eye-icon">
                        </div>
                    </div>
                    <div class="mt-6">
                        <p class="text-gray-600 text-center text-sm sm:text-base">
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
                        class="absolute -top-5 left-1/2 bg-#FDFFEB transform -translate-x-1/2 w-14 h-14 rounded-full  shadow-md flex items-center justify-center">
                        <div class="w-8 h-8 rounded-full  flex items-center justify-center">
                            <img src="@/public/target.png" alt="target-icon">
                        </div>
                    </div>
                    <div class="mt-6">
                        <p class="text-gray-600 text-center text-sm sm:text-base">
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
                        class="absolute -top-5 left-1/2 bg-#DDF9FF transform -translate-x-1/2 w-14 h-14 rounded-full  shadow-md flex items-center justify-center">
                        <div class="w-8 h-8 rounded-full  flex items-center justify-center">
                            <img src="@/public/circle.png" alt="circle-icon">
                        </div>
                    </div>
                    <div class="mt-6">
                        <p class="text-gray-600 text-center text-sm sm:text-base">
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
        <section class="mb-16 md:mb-24 animate-section stats-section">
            <h2 class="text-2xl md:text-3xl font-bold text-center mb-4">THÀNH TÍCH</h2>
            <p class="text-center text-gray-600 mb-8 md:mb-12 max-w-3xl mx-auto">
                Innovator Academy chính thức trở thành đơn vị đào tạo đầu tiên tại Việt Nam được kiểm định và cấp
                <span class="text-#FCAF17 font-bold">Chứng nhận đào tạo</span> về Thương mại điện tử từ cơ quan quản lý
                nhà nước.
            </p>

            <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-4 md:gap-6">
                <div v-for="(stat, index) in stats" :key="index"
                    class="text-center p-4 transition duration-300 hover:scale-105 animate-item"
                    :class="`delay-${index * 100}`">
                    <div class="text-36px md:text-50px font-bold text-#B4CD26 odometer-wrapper">
                        <span class="odometer">{{ stat.current }}</span>{{ stat.unit }}
                    </div>
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

    <!-- Updated "Khoảnh khắc" section with consistent animations -->
    <div class="bg-#FFFBF1 mb-40px">
        <div class="max-w-6xl mx-auto px-4 py-8 font-sans animate-section">
            <h2 class="text-2xl md:text-30px font-bold text-center my-10 text-gray-800">
                Khoảnh khắc tại Innovator Academy
            </h2>

            <!-- Image Gallery -->
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 md:gap-6 mb-16">
                <div v-for="(image, index) in images" :key="image.id"
                    class="rounded-lg overflow-hidden shadow-md animate-item" :class="`delay-${index * 100}`">
                    <img :src="image.src" :alt="image.alt" class="w-full h-64 object-cover" />
                </div>
            </div>
        </div>
    </div>

    <!-- Call to Action Banner -->
    <div class="max-w-6xl mx-auto px-4 pt-8 pb-80px font-sans">
        <div class="bg-gray-100 rounded-lg p-6 md:p-8 shadow-md animate-section">
            <div class="flex flex-col md:flex-row items-start md:items-center justify-between gap-16">
                <div>
                    <h2 class="text-24px md:text-32px font-semibold text-gray-800"><span class="text-#FCAF17">Cùng
                            nhau</span>, hãy định hình tương lai của đổi mới kỹ thuật số
                    </h2>
                    <p class="mt-2 text-gray-600 text-sm md:text-base">
                        Hãy tham gia cùng chúng tôi trong hành trình học tập thú vị này và nhận phần thưởng cấp bậc
                    </p>
                </div>
                <button
                    class="mt-4 min-w-160px md:mt-0 px-4 py-2 bg-#FCAF17 text-white font-medium rounded-md hover:bg-amber-400 transition-all duration-300 transform hover:scale-105 animate-item">
                    Đăng ký ngay
                </button>
            </div>
        </div>
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

/* Odometer animation styling */
.odometer-wrapper {
    display: inline-flex;
    align-items: center;
    justify-content: center;
}

.odometer {
    display: inline-block;
    font-variant-numeric: tabular-nums;
    font-feature-settings: "tnum";
    /* Ensures numbers are monospaced */
    transition: color 0.2s ease;
}

.odometer.highlight {
    color: #fbbf24;
    /* Temporarily highlights changing digits */
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