<script lang="ts" setup>
import { ref, onMounted, nextTick } from 'vue';

interface TrainingMethod {
    title: string;
    description: string;
}

// Define training methods
const methods: TrainingMethod[] = [
    {
        title: 'Hỗ trợ cá nhân hoá',
        description: 'Mỗi học viên sẽ nhận được sự hỗ trợ cá nhân hóa từ các chuyên gia, giúp giải quyết những khó khăn cụ thể và định hướng phát triển phù hợp. Chúng tôi luôn lắng nghe và đáp ứng nhu cầu của từng học viên để đảm bảo họ đạt được mục tiêu học tập và nghề nghiệp.'
    },
    {
        title: 'Cung cấp công cụ quản lý dự án',
        description: 'Innovator Academy cung cấp các công cụ quản lý dự án tiên tiến giúp học viên theo dõi tiến độ và hiệu quả công việc một cách chính xác và tiện lợi.'
    },
    {
        title: 'Nền tảng học trực tuyến',
        description: 'Hệ thống học trực tuyến của chúng tôi được thiết kế để tối ưu hóa trải nghiệm học tập, giúp học viên tiếp cận kiến thức mọi lúc, mọi nơi. Các bài giảng, tài liệu học tập và bài tập thực hành đều được tích hợp trên nền tảng này.'
    },
    {
        title: 'Phần mềm, công cụ hỗ trợ kinh doanh',
        description: 'Học viên sẽ được giới thiệu và hướng dẫn sử dụng các phần mềm hỗ trợ kinh doanh phổ biến như công cụ phân tích thị trường, quản lý kho hàng, chạy quảng cáo PPC và nhiều công cụ khác để tăng hiệu quả kinh doanh.'
    },
    {
        title: 'Cập nhật kiến thức liên tục',
        description: 'Chúng tôi cam kết cung cấp cho học viên những kiến thức mới nhất và cập nhật thường xuyên về các xu hướng và thay đổi của thị trường. Điều này đảm bảo học viên luôn đi đầu trong lĩnh vực kinh doanh của mình.'
    },
    {
        title: 'Thay đổi thị trường',
        description: 'Innovator Academy luôn theo sát những biến động của thị trường, từ đó điều chỉnh nội dung đào tạo để phù hợp với thực tiễn. Học viên sẽ được trang bị những kỹ năng và kiến thức mới nhất để thích ứng và phát triển trong môi trường kinh doanh năng động.'
    }
];

// Create refs for animation
const methodRefs = ref<(HTMLElement | null)[]>([]);

// Initialize animations when component is mounted
onMounted(() => {
    nextTick(() => {
        initAnimations();
    });
});

// Set up intersection observer for scroll animations
const initAnimations = () => {
    if (typeof window === 'undefined' || !window.IntersectionObserver) return;

    const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                // Add animation classes when element is in view
                entry.target.classList.add('opacity-100');
                entry.target.classList.add('translate-y-0');
                observer.unobserve(entry.target);
            }
        });
    }, {
        threshold: 0.2,
        rootMargin: '0px 0px -50px 0px'
    });

    // Observe all method cards
    methodRefs.value.forEach((el) => {
        if (el) {
            observer.observe(el);
        }
    });
};
</script>

<template>
    <div class="w-full px-4 md:px-12 lg:px-[200px]">
        <div class="flex flex-col gap-12 lg:gap-20">
            <h1 class="text-36px font-bold text-gray-800">Phương pháp đào tạo</h1>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <div v-for="(method, index) in methods" :key="index"
                    class="bg-white rounded-2xl border border-gray-200 p-6 transform transition duration-300 ease-in-out hover:-translate-y-2 opacity-0"
                    :ref="el => { if (el) methodRefs[index] = el }">
                    <div class="text-50px font-bold text-right text-amber-500 mb-6">{{ String(index + 1).padStart(2, '0') }}</div>
                    <h3 class="text-lg font-bold text-gray-800 mb-3">{{ method.title }}</h3>
                    <p class="text-gray-500 leading-relaxed text-base">{{ method.description }}</p>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
/* Custom animation styles that complement Tailwind */
.opacity-0 {
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.6s ease-out, transform 0.6s ease-out;
}

.opacity-100 {
    opacity: 1;
    transform: translateY(0);
}

/* Individual delay for each card */
.grid>div:nth-child(1) {
    transition-delay: 0.1s;
}

.grid>div:nth-child(2) {
    transition-delay: 0.25s;
}

.grid>div:nth-child(3) {
    transition-delay: 0.4s;
}

.grid>div:nth-child(4) {
    transition-delay: 0.55s;
}

.grid>div:nth-child(5) {
    transition-delay: 0.7s;
}

.grid>div:nth-child(6) {
    transition-delay: 0.85s;
}
</style>