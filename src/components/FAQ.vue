<script setup lang="ts">
import { ref } from 'vue';

interface FaqItem {
    question: string;
    answer: string;
}

const faqItems: FaqItem[] = [
    {
        question: 'Làm thế nào để đăng ký khoá học?',
        answer: 'Bạn có thể đăng ký khoá học trực tiếp trên website của chúng tôi bằng cách chọn khoá học mong muốn, nhấp vào nút "Đăng ký" và làm theo hướng dẫn thanh toán. Nếu gặp khó khăn, vui lòng liên hệ với chúng tôi qua trang Liên hệ.'
    },
    {
        question: 'Các khoá học được tổ chức như thế nào?',
        answer: 'Các khóa học của chúng tôi được tổ chức trực tuyến với các bài giảng video, tài liệu học tập, bài tập thực hành và diễn đàn thảo luận. Học viên có thể học theo tiến độ của mình và nhận được hỗ trợ từ giảng viên trong suốt quá trình học.'
    },
    {
        question: 'Tôi có thể truy cập khoá học ở đâu?',
        answer: 'Sau khi đăng ký thành công, bạn có thể truy cập khóa học thông qua tài khoản cá nhân trên website của chúng tôi. Bạn có thể học mọi lúc, mọi nơi trên các thiết bị có kết nối internet.'
    },
    {
        question: 'Tôi có thể học theo tiến độ của mình không?',
        answer: 'Vâng, tất cả các khóa học của chúng tôi đều cho phép bạn học theo tiến độ riêng. Bạn có thể tạm dừng, tiếp tục và xem lại nội dung bất kỳ lúc nào trong thời gian khóa học có hiệu lực.'
    },
    {
        question: 'Tôi có được hoàn tiền nếu không hài lòng về khoá học không?',
        answer: 'Chúng tôi cung cấp chính sách hoàn tiền trong vòng 7 ngày kể từ ngày mua khóa học nếu bạn không hài lòng với nội dung. Vui lòng liên hệ với bộ phận hỗ trợ của chúng tôi để được hướng dẫn quy trình hoàn tiền.'
    }
];

const openIndex = ref<number | null>(0); // First item open by default

const toggleItem = (index: number) => {
    openIndex.value = openIndex.value === index ? null : index;
};
</script>

<template>
    <div class="w-full px-6 md:px-[10%] lg:px-[20%] py-[60px] md:py-[80px] overflow-hidden">
        <div class="bg-[#FFFBF1] p-20px md:p-[100px] flex flex-col md:flex-row md:gap-[40px] lg:gap-[80px]">
            <div class="w-full md:w-[40%] lg:w-[30%] mb-8 md:mb-0">
                <h2 class="text-2xl font-bold mb-8 text-gray-900">Câu hỏi thường gặp</h2>
                <p class="mb-4 text-gray-600">
                    Nếu có câu hỏi khác, vui lòng liên hệ với chúng tôi qua hòm thư:
                    <a href="mailto:innovatoracademy@gmail.com" class="hover:text-blue-800">
                        innovatoracademy@gmail.com
                    </a>
                </p>
            </div>

            <div class="space-y-4 w-full md:w-[60%] lg:w-[60%]">
                <div v-for="(item, index) in faqItems" :key="index"
                    class="border border-gray-200 rounded-lg overflow-hidden bg-white shadow-sm">
                    <button @click="toggleItem(index)"
                        class="w-full flex items-center justify-between px-6 py-4 text-left focus:outline-none"
                        :aria-expanded="openIndex === index">
                        <span class="font-medium text-gray-900">{{ index + 1 }}. {{ item.question }}</span>
                        <span class="ml-6 flex-shrink-0">
                            <svg :class="{ 'rotate-180': openIndex === index }"
                                class="h-5 w-5 text-yellow-500 transform transition-transform duration-500 ease-in-out"
                                xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                                <path fill-rule="evenodd"
                                    d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                                    clip-rule="evenodd" />
                            </svg>
                        </span>
                    </button>
                    <div class="overflow-hidden transition-all duration-500 ease-in-out" :class="{
                        'max-h-0 opacity-0': openIndex !== index,
                        'max-h-[500px] opacity-100': openIndex === index
                    }">
                        <div class="px-6 pb-4">
                            <p class="text-gray-600">{{ item.answer }}</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
/* Additional smooth animation for chevron */
svg {
    transition: transform 0.5s cubic-bezier(0.4, 0, 0.2, 1);
}
</style>