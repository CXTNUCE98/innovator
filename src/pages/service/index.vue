<script setup lang="ts">
import { ref, onMounted, nextTick } from 'vue'

// Animation state
const isVisible = ref(false)

// Simple animation setup
const setupScrollAnimations = () => {
    // Trigger animations after a short delay to simulate scroll
    setTimeout(() => {
        isVisible.value = true
    }, 300)
}

onMounted(() => {
    nextTick(() => {
        setupScrollAnimations()
    })
})

const mainOperation = [
    {
        name: 'GÓI RE-REVIEW & EVALUATION',
        price: '156$',
        period: '/tháng',
        benefits: [
            'Chuyên gia đánh giá về sản phẩm/dịch vụ',
            'Tính phù hợp để bán hàng trên Amazon',
            'Đánh giá mức độ cạnh tranh của ngành hàng',
            'Tham vấn phương án triển khai tổng thể',
        ],
        button: 'Đăng ký',
    },
    {
        name: 'LOCAL PACK',
        price: '79$',
        period: '/tháng',
        benefits: [
            'Dịch vụ đăng ký bảo hộ nhãn hiệu',
            'Dịch vụ đại diện đăng ký thuế giá trị gia tăng phạm tại thị trường Mỹ',
            'Dịch vụ đăng ký tư vấn kinh doanh',
        ],
        button: 'Đăng ký',
    },
]

const operationServices = [
    {
        name: 'GÓI GIẢI PHÁP ĐA KÊNH PLATIUM',
        price: '156$',
        period: '/tháng',
        benefits: [
            'Đăng ký tài khoản dựa theo thông tin chính chủ (doanh nghiệp/cá nhân..)',
            'Tạo trang bán hàng chuyên nghiệp',
            'Listing sản phẩm (Phía công ty cần cung cấp thông tin hồ sơ, chuẩn bị hình ảnh sản phẩm cụ thể theo yêu cầu để đảm bảo quá trình triển khai)',
        ],
        button: 'Đăng ký',
    },
    {
        name: 'GÓI GIẢI PHÁP KÊNH QUỐC TẾ TITAN',
        price: '79$',
        period: '/tháng',
        benefits: [
            'Đăng ký tài khoản dựa theo thông tin chính chủ (doanh nghiệp/cá nhân..)',
            'Nghiên cứu phân tích ngách sản phẩm trên Amazon',
            'Thiết kế gian hàng Amazon Content A+ (Phía công ty cần cung cấp thông tin hồ sơ, chuẩn bị hình ảnh sản phẩm cụ thể theo yêu cầu để đảm bảo quá trình triển khai)',
        ],
        button: 'Đăng ký',
    },
    {
        name: 'GÓI ĐẶC HÀNH KÊNH QUỐC TẾ DIAMOND',
        price: '79$',
        period: '/tháng',
        benefits: [
            'Đăng ký tài khoản dựa theo thông tin chính chủ (doanh nghiệp/cá nhân..)',
            'Nghiên cứu phân tích ngách sản phẩm trên Amazon',
            'Thiết kế gian hàng Amazon Content A+',
            'Quản lý tồn kho nền tảng Amazon',
            'Chạy Ads PPC (Pay-per-click)',
            'Quản lý vận hàng bán hàng Dropship FBM &FBA',
        ],
        button: 'Đăng ký',
    },
]

const coachingServices = [
    {
        name: 'Đào tạo 1:1 (6 tháng)',
        price: '156$',
        period: '/tháng',
        benefits: [
            'Đào tạo toàn bộ các modules về kinh doanh trên Amazon cho cá nhân, team và support theo timeline đưa ra',
            'Tư vấn chiến lược cơ bẩn phát triển thương hiệu tại Mỹ thông qua nền tảng Amazon',
            'Support cá nhân, team bán hàng trên Amazon (VD: Support tối ưu QC, quản lý hàng hoá, vận chuyển...)',
            'Tặng 01 buổi đào tạo chuyên sâu',
        ],
        button: 'Đăng ký',
    },
    {
        name: 'Đào tạo 1:1 nâng cao và chuyển giao (3 - 6 tháng)',
        price: '79$',
        period: '/tháng',
        benefits: [
            'Đào tạo toàn bộ các modules cơ bản và nâng cao về kinh doanh trong và ngoài Amazon cho cá nhân, team và support theo timeline đưa ra',
            'Tư vấn đưa ra chiến lược phát triển thương hiệu tại Mỹ thông qua nền tảng trong và ngoài Amazon',
            'Đồng hành cùng cá nhân, team xây dựng lộ trình phát triển thương hiệu, quản lý hàng tồn kho, xử lý các vấn đề liên quan đến tài khoản, listing …',
            'Support học viên trong quá trình vận hành, VD: chạy Ads trên Amazon, tối ưu hoá quảng cáo, xây dựng các chiến dịch Marketing ngoài Amazon,...',
        ],
        button: 'Đăng ký',
    },
]
</script>

<template>
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-12 md:py-16 lg:py-20">
        <div class="container mx-auto px-2 md:px-0">
            <!-- Nhóm 1: Dịch vụ vận hành triển khai -->
            <section class="animate-section" :class="{ 'visible': isVisible }">
                <h2 class="text-center text-xl md:text-2xl font-bold mb-6 mt-4 animate-item">Dịch vụ vận hành triển khai</h2>

                <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-2 gap-6 mb-12 justify-center">
                    <div v-for="(service, idx) in mainOperation" :key="service.name"
                        class="service-card bg-#FAFAFA rounded-2xl shadow-md border border-gray-100 flex flex-col items-center px-4 py-6 min-h-[420px] animate-item"
                        :style="{ animationDelay: `${idx * 0.2}s` }">
                        <div
                            class="w-full bg-#FFEDCC rounded-lg py-2 text-center mb-4 font-semibold text-gray-800 text-sm tracking-wide border-b border-yellow-100">
                            {{ service.name }}</div>
                        <div class="text-4xl font-bold text-gray-900 mb-1">{{ service.price }}<span
                                class="text-lg font-normal">{{ service.period }}</span></div>
                        <div class="relative text-left bg-#FFF w-full mt-2 mb-4 px-4 md:px-8 py-4 h-full flex flex-col">
                            <div class="font-semibold mb-2 text-gray-800">Quyền lợi</div>
                            <ul class="space-y-2 flex-1">
                                <li v-for="benefit in service.benefits" :key="benefit"
                                    class="flex items-start text-gray-700 text-sm">
                                    <svg class="w-5 h-5 text-yellow-400 mr-2 mt-0.5 flex-shrink-0" fill="none"
                                        stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
                                    </svg>
                                    <span>{{ benefit }}</span>
                                </li>
                            </ul>
                            <button
                                class="mt-4 w-full bg-gradient-to-r from-yellow-400 to-orange-400 hover:from-yellow-500 hover:to-orange-500 text-white font-semibold py-2 rounded-lg shadow transition transform duration-200">{{
                                    service.button }}</button>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Nhóm 2: Dịch vụ vận hành triển khai -->
            <section class="animate-section" :class="{ 'visible': isVisible }">
                <div class="grid grid-cols-1 bg-#FAFAFA sm:grid-cols-2 md:grid-cols-3 gap-6 mb-12">
                    <div v-for="(service, idx) in operationServices" :key="service.name"
                        class="service-card bg-#FAFAFA rounded-2xl shadow-md border border-gray-100 flex flex-col items-center px-4 py-6 min-h-[420px] animate-item"
                        :style="{ animationDelay: `${idx * 0.15}s` }">
                        <div
                            class="w-full bg-#FFEDCC rounded-lg py-2 text-center mb-4 font-semibold text-gray-800 text-sm tracking-wide border-b border-yellow-100">
                            {{ service.name }}</div>
                        <div class="text-4xl font-bold text-gray-900 mb-1">{{ service.price }}<span
                                class="text-lg font-normal">{{ service.period }}</span></div>
                        <div class="text-left bg-#FFF w-full mt-2 mb-4 px-4 md:px-8 py-4 flex flex-col h-full">
                            <div class="font-semibold mb-2 text-gray-800">Quyền lợi</div>
                            <ul class="space-y-2 flex-1">
                                <li v-for="benefit in service.benefits" :key="benefit"
                                    class="flex items-start text-gray-700 text-sm">
                                    <svg class="w-5 h-5 text-yellow-400 mr-2 mt-0.5 flex-shrink-0" fill="none"
                                        stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
                                    </svg>
                                    <span>{{ benefit }}</span>
                                </li>
                            </ul>
                            <button
                                class="mt-4 w-full bg-gradient-to-r from-yellow-400 to-orange-400 hover:from-yellow-500 hover:to-orange-500 text-white font-semibold py-2 rounded-lg shadow transition transform duration-200">{{
                                    service.button }}</button>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Nhóm 3: Dịch vụ đào tạo coaching và chuyển giao -->
            <section class="animate-section" :class="{ 'visible': isVisible }">
                <h2 class="text-center text-xl md:text-2xl font-bold mb-6 mt-10 animate-item">Dịch vụ đào tạo coaching và chuyển giao
                </h2>
                <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-2 gap-6 mb-12 justify-center">
                    <div v-for="(service, idx) in coachingServices" :key="service.name"
                        class="service-card bg-#FAFAFA rounded-2xl shadow-md border border-gray-100 flex flex-col items-center px-4 py-6 min-h-[420px] animate-item"
                        :style="{ animationDelay: `${idx * 0.2}s` }">
                        <div
                            class="w-full bg-#FFEDCC rounded-lg py-2 text-center mb-4 font-semibold text-gray-800 text-sm tracking-wide border-b border-yellow-100">
                            {{ service.name }}</div>
                        <div class="text-4xl font-bold text-gray-900 mb-1">{{ service.price }}<span
                                class="text-lg font-normal">{{ service.period }}</span></div>
                        <div class="text-left bg-#FFF w-full mt-2 mb-4 px-4 md:px-8 py-4 flex flex-col h-full">
                            <div class="font-semibold mb-2 text-gray-800">Quyền lợi</div>
                            <ul class="space-y-2 flex-1">
                                <li v-for="benefit in service.benefits" :key="benefit"
                                    class="flex items-start text-gray-700 text-sm">
                                    <svg class="w-5 h-5 text-yellow-400 mr-2 mt-0.5 flex-shrink-0" fill="none"
                                        stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
                                    </svg>
                                    <span>{{ benefit }}</span>
                                </li>
                            </ul>
                            <button
                                class="mt-4 w-full bg-gradient-to-r from-yellow-400 to-orange-400 hover:from-yellow-500 hover:to-orange-500 text-white font-semibold py-2 rounded-lg shadow transition transform duration-200">{{
                                    service.button }}</button>
                        </div>
                    </div>
                </div>
            </section>
        </div>
    </div>
</template>

<style scoped>
/* Animation classes */
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

/* Service card animations */
.service-card {
    opacity: 0;
    transform: translateY(40px) scale(0.95);
    transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}

.animate-section.visible .service-card {
    opacity: 1;
    transform: translateY(0) scale(1);
}

/* Button hover animation */
button {
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

button:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 25px rgba(245, 158, 11, 0.3);
}

/* Reduced motion support */
@media (prefers-reduced-motion: reduce) {
    .animate-section,
    .animate-item,
    .service-card,
    button {
        opacity: 1 !important;
        transform: none !important;
        transition: none !important;
    }
    
    .service-card:hover {
        transform: none !important;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1) !important;
    }
}

.playfair-display {
    font-family: 'Playfair Display', serif;
    font-optical-sizing: auto;
}
</style>