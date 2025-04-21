<script setup lang="ts">
import Facebook from "@/public/facebook.png"
import Whatsapp from "@/public/whatsapp.png"
import Telegram from "@/public/telegram.png"
import Twitter from "@/public/twitter.png"

const route = useRoute()
console.log('route: ', route)

// Data
const reasons = [
    'Chi phí khởi nghiệp thấp',
    'Thị trường toàn cầu',
    'Thu nhập không giới hạn',
    'Linh hoạt về địa điểm',
    'Dễ dàng mở rộng kinh doanh',
    'Được hỗ trợ từ chuyên gia'
];

const targetAudience = [
    'Freelancer',
    'Sinh viên',
    'Mẹ bỉm sữa',
    'Người đi làm'
];

const benefits = [
    'Đội ngũ giảng viên giàu kinh nghiệm và chia sẻ thành công của họ',
    'Tham gia vào các bài tập và dự án thực tế để áp dụng kiến thức',
    'Tham gia cộng đồng học viên và được hỗ trợ từ các chuyên gia ngay cả khi hoàn thành khoá học'
];

const socialSharing = [
    { name: 'LinkedIn', icon: Whatsapp },
    { name: 'Facebook', icon: Facebook },
    { name: 'Telegram', icon: Telegram },
    { name: 'Twitter', icon: Twitter },
];

const courseModules = [
    {
        title: 'Giới thiệu về Dropshipping',
        lessons: 2,
        content: [
            'Hiểu rõ về mô hình dropshipping và lý do tại sao nó lại thu hút nhiều người',
            'Cách hoạt động và những bước cơ bản để bắt đầu'
        ]
    },
    {
        title: 'Lựa chọn ngành sản phẩm',
        lessons: 2,
        content: [
            'Cách nghiên cứu thị trường để tìm ra những sản phẩm tiềm năng',
            'Phân tích đối thủ cạnh tranh và xu hướng của thị trường'
        ]
    },
    {
        title: 'Thiết lập cửa hàng trực tuyến',
        lessons: 2,
        content: []
    },
    {
        title: 'Quản lý sản phẩm và nhà cung cấp',
        lessons: 2,
        content: []
    },
    {
        title: 'Chiến lược tiếp thị và bán hàng',
        lessons: 2,
        content: []
    },
    {
        title: 'Quản lý vận hành và hậu cần',
        lessons: 2,
        content: []
    },
    {
        title: 'Phân tích hiệu quả kinh doanh',
        lessons: 2,
        content: []
    }
];

// Reactive state
const activeModules = ref(courseModules.map(() => false));
activeModules.value[0] = true; // First module open by default

const countdown = ref({
    days: '01',
    hours: '12',
    minutes: '43'
});

// Methods
const toggleModule = (index: number) => {
    activeModules.value[index] = !activeModules.value[index];
};

// Animations on scroll
onMounted(() => {
    const elements = document.querySelectorAll('h1, h2, section, .rounded-lg');

    const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.classList.add('animate-fade-in');
                observer.unobserve(entry.target);
            }
        });
    }, { threshold: 0.1 });

    elements.forEach(el => {
        el.classList.add('opacity-0');
        observer.observe(el);
    });

    // Countdown timer
    const timerInterval = setInterval(() => {
        // Just for demo purposes, decrease minutes
        let minutes = parseInt(countdown.value.minutes);
        if (minutes > 0) {
            minutes--;
            countdown.value.minutes = minutes.toString().padStart(2, '0');
        } else {
            countdown.value.minutes = '59';

            let hours = parseInt(countdown.value.hours);
            if (hours > 0) {
                hours--;
                countdown.value.hours = hours.toString().padStart(2, '0');
            } else {
                countdown.value.hours = '23';

                let days = parseInt(countdown.value.days);
                if (days > 0) {
                    days--;
                    countdown.value.days = days.toString().padStart(2, '0');
                }
            }
        }
    }, 60000); // Update every minute

    onBeforeUnmount(() => {
        clearInterval(timerInterval);
    });

    startCountdown('23/04/2025')
});

const hours = ref()
const minutes = ref()
const seconds = ref()
function startCountdown(targetDateStr) {
    const [day, month, year] = targetDateStr.split("/").map(Number);
    let targetDate = new Date(year, month - 1, day);

    function updateCountdown() {
        const now = new Date();
        let diff = targetDate - now;

        if (diff <= 0) {
            // Nếu đã hết thời gian, cộng thêm 3 ngày
            targetDate.setDate(targetDate.getDate() + 3);
            diff = targetDate - now;
        }

        hours.value = Math.floor(diff / (1000 * 60 * 60));
        minutes.value = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
        seconds.value = Math.floor((diff % (1000 * 60)) / 1000);

        console.log(
            `Countdown to ${targetDate.toLocaleDateString()} → ${String(hours).padStart(2, "0")} : ${String(minutes).padStart(2, "0")} : ${String(seconds).padStart(2, "0")}`
        );

        return { hours, minutes, seconds, nextTarget: targetDate };
    }

    setInterval(updateCountdown, 1000);
}
</script>

<template>
    <main class="max-w-6xl mx-auto mt-64px px-4 py-8 md:py-12">
        <div class="hidden md:block pb-32px">
            <i class='bx bx-arrow-back rounded-full bg-#F5F5F5 p-2 text-20px '></i>
        </div>
        <div class="flex lg:flex-row flex-col-reverse gap-8 ">
            <!-- Left Content Section -->
            <div class="space-y-8">
                <h1 class="text-3xl md:text-4xl font-bold text-gray-800 transition-all duration-300 hover:text-indigo-600">
                    Khoá học Dropship
                </h1>

                <p class="text-gray-600 leading-relaxed">
                    Khoá học Dropship tại Innovator Academy được thiết kế để giúp bạn bước chân vào thế giới kinh doanh trực
                    tuyến một cách dễ dàng và hiệu quả. Với phương pháp giảng dạy sinh động, chúng tôi sẽ dẫn dắt bạn từ
                    những bước đầu tiên đến khi bạn có thể tự tin quản lý một cửa hàng dropshipping thành công.
                </p>

                <section>
                    <h2 class="text-xl md:text-2xl font-semibold text-gray-800 mb-4">Tại sao nên học kinh doanh Dropship
                    </h2>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div v-for="(reason, index) in reasons" :key="`reason-${index}`"
                            class="flex items-start space-x-2 group">
                            <div
                                class="flex-shrink-0 w-5 h-5 rounded-full bg-yellow-400 flex items-center justify-center mt-1 transform transition-all group-hover:rotate-12">
                                <CheckIcon class="w-3 h-3 text-white" />
                            </div>
                            <span class="text-gray-700 group-hover:text-indigo-600 transition-colors">{{ reason }}</span>
                        </div>
                    </div>
                </section>

                <section>
                    <h2 class="text-xl md:text-2xl font-semibold text-gray-800 mb-4">Dành cho ai?</h2>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div v-for="(audience, index) in targetAudience" :key="`audience-${index}`"
                            class="flex items-start space-x-2 group">
                            <div
                                class="flex-shrink-0 w-5 h-5 rounded-full bg-yellow-400 flex items-center justify-center mt-1 transform transition-all group-hover:rotate-12">
                                <CheckIcon class="w-3 h-3 text-white" />
                            </div>
                            <span class="text-gray-700 group-hover:text-indigo-600 transition-colors">{{ audience }}</span>
                        </div>
                    </div>
                </section>

                <section>
                    <h2 class="text-xl md:text-2xl font-semibold text-gray-800 mb-4">Được gì khi tham gia khoá học?</h2>

                    <div class="space-y-4">
                        <div v-for="(benefit, index) in benefits" :key="`benefit-${index}`"
                            class="flex items-start space-x-2 group">
                            <div
                                class="flex-shrink-0 w-5 h-5 rounded-full bg-yellow-400 flex items-center justify-center mt-1 transform transition-all group-hover:rotate-12">
                                <CheckIcon class="w-3 h-3 text-white" />
                            </div>
                            <span class="text-gray-700 group-hover:text-indigo-600 transition-colors">{{ benefit }}</span>
                        </div>
                    </div>
                </section>

                <!-- Course Content Section -->
                <section class="mt-12 md:mt-16">
                    <h2 class="text-2xl font-semibold text-gray-800 flex items-center justify-between">
                        Nội dung khoá học
                        <button class="text-yellow-500 hover:text-yellow-600 text-sm flex items-center space-x-1">
                            <span>Mở rộng toàn bộ</span>
                            <ChevronDownIcon class="w-4 h-4" />
                        </button>
                    </h2>

                    <div class="mt-6 space-y-4">
                        <div v-for="(module, index) in courseModules" :key="`module-${index}`"
                            class="border border-gray-200 rounded-lg overflow-hidden">
                            <div class="bg-gray-50 p-4 flex items-center justify-between cursor-pointer hover:bg-gray-100 transition-colors"
                                @click="toggleModule(index)">
                                <div class="flex items-center space-x-3">
                                    <div
                                        class="w-6 h-6 rounded-full bg-gray-200 flex items-center justify-center text-gray-700 font-medium">
                                        {{ index + 1 }}
                                    </div>
                                    <h3 class="font-medium">{{ module.title }}</h3>
                                </div>

                                <div class="flex items-center space-x-2">
                                    <span class="text-sm text-gray-500">{{ module.lessons }} bài học</span>
                                    <ChevronDownIcon
                                        :class="['w-5 h-5 transition-transform', { 'transform rotate-180': activeModules[index] }]" />
                                </div>
                            </div>

                            <div v-show="activeModules[index]" class="p-4 border-t border-gray-200 space-y-3">
                                <div v-for="(lesson, lIndex) in module.content" :key="`lesson-${index}-${lIndex}`"
                                    class="flex items-start space-x-2 py-2 group">
                                    <div
                                        class="flex-shrink-0 w-5 h-5 rounded-full bg-yellow-400 flex items-center justify-center mt-1">
                                        <div class="w-2 h-2 bg-white rounded-full"></div>
                                    </div>
                                    <span class="text-gray-700 group-hover:text-indigo-600 transition-colors">{{ lesson
                                    }}</span>
                                </div>
                            </div>

                        </div>
                    </div>

                    <div
                        class="self-stretch p-6 bg-Background-Background-gray rounded-2xl inline-flex flex-col justify-start items-center gap-10">
                        <div
                            class="self-stretch pb-6 border-b border-Border-Border-default flex flex-col justify-start items-start gap-4">
                            <div
                                class="justify-start text-Text&Icon-Text-title text-2xl font-bold font-['Inter'] leading-loose">
                                Đánh giá </div>
                            <div class="inline-flex justify-start items-center gap-6">
                                <div data-rate="5 star" data-size="XL" class="flex justify-start items-start gap-2">
                                    <div data-badge="false" data-size="32x32"
                                        class="inline-flex flex-col justify-start items-start">
                                        <div class="w-8 h-8 relative rounded-lg">
                                            <div class="w-8 h-8 left-0 top-0 absolute overflow-hidden">
                                                <div class="w-7 h-6 left-[2.67px] top-[3.34px] absolute bg-Warning-Warning">
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                    <div data-badge="false" data-size="32x32"
                                        class="inline-flex flex-col justify-start items-start">
                                        <div class="w-8 h-8 relative rounded-lg">
                                            <div class="w-8 h-8 left-0 top-0 absolute overflow-hidden">
                                                <div class="w-7 h-6 left-[2.67px] top-[3.34px] absolute bg-Warning-Warning">
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                    <div data-badge="false" data-size="32x32"
                                        class="inline-flex flex-col justify-start items-start">
                                        <div class="w-8 h-8 relative rounded-lg">
                                            <div class="w-8 h-8 left-0 top-0 absolute overflow-hidden">
                                                <div class="w-7 h-6 left-[2.67px] top-[3.34px] absolute bg-Warning-Warning">
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                    <div data-badge="false" data-size="32x32"
                                        class="inline-flex flex-col justify-start items-start">
                                        <div class="w-8 h-8 relative rounded-lg">
                                            <div class="w-8 h-8 left-0 top-0 absolute overflow-hidden">
                                                <div class="w-7 h-6 left-[2.67px] top-[3.34px] absolute bg-Warning-Warning">
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                    <div data-badge="false" data-size="32x32"
                                        class="inline-flex flex-col justify-start items-start">
                                        <div class="w-8 h-8 relative rounded-lg">
                                            <div class="w-8 h-8 left-0 top-0 absolute overflow-hidden">
                                                <div class="w-7 h-6 left-[2.67px] top-[3.34px] absolute bg-Warning-Warning">
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                                <div class="flex justify-start items-center gap-4">
                                    <div
                                        class="justify-start text-Text&Icon-Text-label text-xl font-bold font-['Inter'] leading-7">
                                        5 .0</div>
                                    <div
                                        class="justify-start text-Text&Icon-Text-title text-sm font-normal font-['Inter'] leading-tight">
                                        20 lượt đánh giá</div>
                                </div>
                            </div>
                        </div>
                        <div class="self-stretch flex flex-col justify-start items-start gap-6">
                            <div class="self-stretch inline-flex justify-start items-start gap-4">
                                <div class="flex-1 flex justify-start items-center gap-4">
                                    <div
                                        class="w-16 h-16 relative bg-Background-Background-gray-3 rounded-[33px] border-[3px] border-white">
                                    </div>
                                    <div class="inline-flex flex-col justify-start items-start gap-2">
                                        <div
                                            class="w-36 h-6 justify-center text-Text&Icon-Text-label text-xl font-bold font-['Inter'] leading-7">
                                            Huy Đặng</div>
                                        <div class="inline-flex justify-start items-center gap-4">
                                            <div data-rate="5 star" data-size="S"
                                                class="flex justify-start items-start gap-1">
                                                <div data-badge="false" data-size="16x16"
                                                    class="flex justify-center items-center gap-2">
                                                    <div class="w-4 h-4 relative rounded-lg">
                                                        <div class="w-4 h-4 left-0 top-0 absolute overflow-hidden">
                                                            <div
                                                                class="w-3.5 h-3 left-[1.33px] top-[1.67px] absolute bg-Warning-Warning">
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                <div data-badge="false" data-size="16x16"
                                                    class="flex justify-center items-center gap-2">
                                                    <div class="w-4 h-4 relative rounded-lg">
                                                        <div class="w-4 h-4 left-0 top-0 absolute overflow-hidden">
                                                            <div
                                                                class="w-3.5 h-3 left-[1.33px] top-[1.67px] absolute bg-Warning-Warning">
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                <div data-badge="false" data-size="16x16"
                                                    class="flex justify-center items-center gap-2">
                                                    <div class="w-4 h-4 relative rounded-lg">
                                                        <div class="w-4 h-4 left-0 top-0 absolute overflow-hidden">
                                                            <div
                                                                class="w-3.5 h-3 left-[1.33px] top-[1.67px] absolute bg-Warning-Warning">
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                <div data-badge="false" data-size="16x16"
                                                    class="flex justify-center items-center gap-2">
                                                    <div class="w-4 h-4 relative rounded-lg">
                                                        <div class="w-4 h-4 left-0 top-0 absolute overflow-hidden">
                                                            <div
                                                                class="w-3.5 h-3 left-[1.33px] top-[1.67px] absolute bg-Warning-Warning">
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                <div data-badge="false" data-size="16x16"
                                                    class="flex justify-center items-center gap-2">
                                                    <div class="w-4 h-4 relative rounded-lg">
                                                        <div class="w-4 h-4 left-0 top-0 absolute overflow-hidden">
                                                            <div
                                                                class="w-3.5 h-3 left-[1.33px] top-[1.67px] absolute bg-Warning-Warning">
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                                <div
                                    class="justify-center text-Text&Icon-Text-label text-sm font-normal font-['Inter'] leading-tight">
                                    24/06/2024</div>
                            </div>
                            <div
                                class="w-[610px] justify-center text-Text&Icon-Text-label text-base font-normal font-['Inter'] leading-normal">
                                “Khoá học rất hữu ích và dễ hiểu. Tôi đã học được rất nhiều kiến thức mới</div>
                        </div>
                        <div class="self-stretch flex flex-col justify-start items-start gap-6">
                            <div class="self-stretch inline-flex justify-start items-start gap-4">
                                <div class="flex-1 flex justify-start items-center gap-4">
                                    <div
                                        class="w-16 h-16 relative bg-Background-Background-gray-3 rounded-[33px] border-[3px] border-white">
                                    </div>
                                    <div class="inline-flex flex-col justify-start items-start gap-2">
                                        <div
                                            class="w-36 h-6 justify-center text-Text&Icon-Text-label text-xl font-bold font-['Inter'] leading-7">
                                            Huy Đặng</div>
                                        <div class="inline-flex justify-start items-center gap-4">
                                            <div data-rate="5 star" data-size="S"
                                                class="flex justify-start items-start gap-1">
                                                <div data-badge="false" data-size="16x16"
                                                    class="flex justify-center items-center gap-2">
                                                    <div class="w-4 h-4 relative rounded-lg">
                                                        <div class="w-4 h-4 left-0 top-0 absolute overflow-hidden">
                                                            <div
                                                                class="w-3.5 h-3 left-[1.33px] top-[1.67px] absolute bg-Warning-Warning">
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                <div data-badge="false" data-size="16x16"
                                                    class="flex justify-center items-center gap-2">
                                                    <div class="w-4 h-4 relative rounded-lg">
                                                        <div class="w-4 h-4 left-0 top-0 absolute overflow-hidden">
                                                            <div
                                                                class="w-3.5 h-3 left-[1.33px] top-[1.67px] absolute bg-Warning-Warning">
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                <div data-badge="false" data-size="16x16"
                                                    class="flex justify-center items-center gap-2">
                                                    <div class="w-4 h-4 relative rounded-lg">
                                                        <div class="w-4 h-4 left-0 top-0 absolute overflow-hidden">
                                                            <div
                                                                class="w-3.5 h-3 left-[1.33px] top-[1.67px] absolute bg-Warning-Warning">
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                <div data-badge="false" data-size="16x16"
                                                    class="flex justify-center items-center gap-2">
                                                    <div class="w-4 h-4 relative rounded-lg">
                                                        <div class="w-4 h-4 left-0 top-0 absolute overflow-hidden">
                                                            <div
                                                                class="w-3.5 h-3 left-[1.33px] top-[1.67px] absolute bg-Warning-Warning">
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                <div data-badge="false" data-size="16x16"
                                                    class="flex justify-center items-center gap-2">
                                                    <div class="w-4 h-4 relative rounded-lg">
                                                        <div class="w-4 h-4 left-0 top-0 absolute overflow-hidden">
                                                            <div
                                                                class="w-3.5 h-3 left-[1.33px] top-[1.67px] absolute bg-Warning-Warning">
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                                <div
                                    class="justify-center text-Text&Icon-Text-label text-sm font-normal font-['Inter'] leading-tight">
                                    24/06/2024</div>
                            </div>
                            <div
                                class="w-[567px] justify-center text-Text&Icon-Text-label text-base font-normal font-['Inter'] leading-normal">
                                “Khoá học rất hữu ích và dễ hiểu. Tôi đã học được rất nhiều kiến thức mới</div>
                        </div>
                        <div data-circle-button="No" data-left-icon="false" data-level="Primary" data-right-icon="true"
                            data-size="48px" data-status="Active" data-style="Text" data-text="Yes"
                            class="px-6 py-3 rounded-lg inline-flex justify-center items-center gap-2">
                            <div
                                class="text-center justify-start text-Primary-Primary text-base font-medium font-['Inter'] leading-normal">
                                Xem thêm</div>
                            <div class="w-6 h-6 relative">
                                <div class="w-4 h-2 left-[4.25px] top-[7.75px] absolute bg-Primary-Primary"></div>
                            </div>
                        </div>
                    </div>
                </section>
            </div>

            <!-- Right Image & Course Details Section -->
            <div class="flex flex-col space-y-6 ">
                <div class="rounded-lg overflow-hidden bg-neutral-50 shadow-lg transform transition-all ">
                    <div class="rounded-16px">
                        <img src="https://www.globalcareercounsellor.com/blog/wp-content/uploads/2018/05/Online-Career-Counselling-course.jpg"
                            alt="Dropship course" class="w-full h-auto object-cover p-4 rounded-26px" />
                    </div>

                    <div class="p-4 relative">
                        <!-- Course Card -->
                        <div
                            class="self-stretch p-4 bg-gradient-to-r from-red-600 to-red-500 rounded-lg flex flex-col justify-start items-start gap-3">
                            <div class="self-stretch inline-flex justify-between items-start">
                                <div class="flex-1 inline-flex flex-col justify-center items-start gap-1">
                                    <div class="inline-flex justify-start items-center gap-1">
                                        <div class="w-5 h-5 relative overflow-hidden">
                                            <!-- <div class="w-2.5 h-4 left-[5px] top-[1.67px] absolute bg-Yellow-Yellow"></div> -->
                                            <img src="../../public/thunder.png" alt="">
                                        </div>
                                        <div
                                            class="justify-start text-white text-xs font-medium font-['Inter'] leading-none tracking-tight">
                                            Ưu đãi đặc biệt</div>
                                    </div>
                                    <div class="inline-flex justify-start items-center gap-1.5">
                                        <div
                                            class="justify-start text-white text-xl font-medium font-['Inter'] leading-loose tracking-tight">
                                            11.290.000đ</div>
                                    </div>
                                    <div class="inline-flex justify-start items-center gap-1">
                                        <div
                                            class="opacity-50 justify-start text-white text-xs font-medium font-['Inter'] line-through leading-none">
                                            15.720.000đ</div>
                                        <div
                                            class="px-1 py-0.5 bg-rose-50 rounded-md flex justify-center items-center gap-2.5">
                                            <div
                                                class="justify-start text-red-600 text-xs font-medium font-['Inter'] leading-none tracking-tight">
                                                -25%</div>
                                        </div>
                                    </div>
                                </div>
                                <div class="flex-1 self-stretch inline-flex flex-col justify-between items-end">
                                    <div
                                        class="justify-start text-white text-xs font-medium font-['Inter'] leading-none tracking-tight">
                                        Kết thúc sau</div>
                                    <div class="inline-flex justify-start items-center gap-1">
                                        <div
                                            class="px-2.5 py-1 bg-white/30 rounded-lg flex justify-center items-end gap-2.5 overflow-hidden">
                                            <div
                                                class="justify-start text-white text-base font-medium font-['Inter'] leading-normal">
                                                {{ hours }} </div>
                                        </div>
                                        <div class="inline-flex flex-col justify-start items-start gap-1">
                                            <div class="w-1 h-1 bg-white rounded-3xl"></div>
                                            <div class="w-1 h-1 bg-white rounded-3xl"></div>
                                        </div>
                                        <div
                                            class="px-2.5 py-1 bg-white/30 rounded-lg flex justify-center items-end gap-2.5 overflow-hidden">
                                            <div
                                                class="justify-start text-white text-base font-medium font-['Inter'] leading-normal">
                                                {{ minutes }}</div>
                                        </div>
                                        <div class="inline-flex flex-col justify-start items-start gap-1">
                                            <div class="w-1 h-1 bg-white rounded-3xl"></div>
                                            <div class="w-1 h-1 bg-white rounded-3xl"></div>
                                        </div>
                                        <div
                                            class="px-2.5 py-1 bg-white/30 rounded-lg flex justify-center items-end gap-2.5 overflow-hidden">
                                            <div
                                                class="justify-start text-white text-base font-medium font-['Inter'] leading-normal">
                                                {{ seconds }}</div>
                                        </div>
                                    </div>
                                    <div class="self-stretch inline-flex justify-end items-center gap-2">
                                        <div
                                            class="justify-start text-white text-xs font-normal font-['Inter'] leading-none tracking-tight">
                                            12 người đã đặt</div>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <div class="mt-4 pt-4  space-y-3">
                            <h3 class="font-semibold text-xl">Khoá học Dropship</h3>

                            <div class="flex items-center space-x-2 text-gray-600">
                                <i class='bx bxs-book-bookmark'></i>
                                <span>32 buổi: 16</span>
                            </div>

                            <div class="flex items-center space-x-2 text-gray-600">
                                <i class='bx bxs-user'></i>
                                <span>Số lượng hs: 16/20</span>
                            </div>

                            <div class="flex items-center space-x-2 text-gray-600">
                                <i class='bx bxs-calendar'></i>
                                <span>Thời gian: Cả tuần</span>
                            </div>

                            <div class="flex items-center space-x-2 text-gray-600">
                                <i class='bx bxs-video'></i>
                                <span>Hình thức: Online</span>
                            </div>

                            <button
                                class="w-full bg-yellow-500 hover:bg-yellow-600 transition-colors text-white font-medium py-3 rounded-lg flex items-center justify-center space-x-2 transform hover:scale-105">
                                <span>Đăng ký ngay</span>
                                <ArrowRightIcon class="w-4 h-4" />
                            </button>
                        </div>

                        <div class="mt-24px pt-4 border-t border-gray-100">
                            <p class="text-sm text-gray-600 mb-16px">Chia sẻ khoá học</p>
                            <div class="flex gap-24px">
                                <div v-for="(social, index) in socialSharing" :key="`social-${index}`"
                                    class="w-8 h-8 rounded-full opacity-100 flex items-center justify-center hover:opacity-90 cursor-pointer transition-colors">
                                    <img :src="social.icon" alt="icon-social">
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

    </main>
</template>

<style>
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

.animate-fade-in {
    animation: fadeIn 0.8s ease-out forwards;
}
</style>