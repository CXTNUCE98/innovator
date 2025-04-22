<script setup lang="ts">
import Facebook from "@/public/facebook.png"
import Whatsapp from "@/public/whatsapp.png"
import Telegram from "@/public/telegram.png"
import Twitter from "@/public/twitter.png"

const route = useRoute()
const idCourse = computed(() => {
    return route?.params.id as string
})

const courseDetail = ref(courses?.find((el) => el.id === idCourse.value))

// Social sharing data
const socialSharing = [
    { name: 'LinkedIn', icon: Whatsapp },
    { name: 'Facebook', icon: Facebook },
    { name: 'Telegram', icon: Telegram },
    { name: 'Twitter', icon: Twitter },
];

// Reactive state
const activeModules = ref(courseDetail.value?.courseModules.map(() => false));
activeModules.value[0] = true;

const countdown = ref({
    days: '01',
    hours: '12',
    minutes: '43'
});

// Methods
const toggleModule = (index: number) => {
    activeModules.value[index] = !activeModules.value[index];
};

function fullyExpanded() {
    courseDetail.value?.courseModules.map((_, index) => activeModules.value[index] = true)
}

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

    startCountdown(courseDetail.value?.promotions?.dateDiscount)
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

        return { hours, minutes, seconds, nextTarget: targetDate };
    }

    setInterval(updateCountdown, 1000);
}


const numberShowFeedback = ref(2)
const isAnimating = ref(false)

// Modified function to show more feedbacks with animation
function handleShowMore() {
    if (isAnimating.value) return; // Prevent multiple clicks during animation

    isAnimating.value = true;

    // Add 2 more feedbacks with animation
    setTimeout(() => {
        numberShowFeedback.value += 2;
        isAnimating.value = false;
    }, 500); // Increased delay for smoother animation
}

// Computed property to get the visible feedbacks
const showFeedbacks = computed(() => {
    return courseDetail.value?.feedbacks.slice(0, numberShowFeedback.value);
})

function formatNumberWithDots(number: string) {
    return number.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".");
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
                <h1 class="text-3xl md:text-4xl font-bold text-gray-800 transition-all duration-300">
                    {{ courseDetail?.title }}
                </h1>

                <p class="text-gray-600 leading-relaxed">
                    {{ courseDetail?.subTitle }}
                </p>

                <section>
                    <h2 class="text-xl md:text-2xl font-semibold text-gray-800 mb-4">{{ courseDetail?.nameModifier }}
                    </h2>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div v-for="(rea, index) in courseDetail?.reason" :key="`rea-${index}`"
                            class="flex items-start space-x-2 group">
                            <div
                                class="flex-shrink-0 w-6 h-6 rounded-full bg-#FFFBF1 flex items-center justify-center mt-1 transform transition-all group-hover:rotate-12">
                                <i class='bx bx-check text-18px' style="color:#FCAF17"></i>
                            </div>
                            <span class="text-gray-700  transition-colors">{{ rea }}</span>
                        </div>
                    </div>
                </section>

                <section>
                    <h2 class="text-xl md:text-2xl font-semibold text-gray-800 mb-4">Dành cho ai?</h2>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div v-for="(audience, index) in courseDetail?.targetAudience" :key="`audience-${index}`"
                            class="flex items-start space-x-2 group">
                            <div
                                class="flex-shrink-0 w-6 h-6 rounded-full bg-#FFFBF1 flex items-center justify-center mt-1 transform transition-all group-hover:rotate-12">
                                <i class='bx bx-check text-18px' style="color:#FCAF17"></i>
                            </div>
                            <span class="text-gray-700  transition-colors">{{ audience }}</span>
                        </div>
                    </div>
                </section>

                <section>
                    <h2 class="text-xl md:text-2xl font-semibold text-gray-800 mb-4">Được gì khi tham gia khoá học?</h2>

                    <div class="space-y-4">
                        <div v-for="(benefit, index) in courseDetail?.benefit" :key="`benefit-${index}`"
                            class="flex items-start space-x-2 group">
                            <div
                                class="flex-shrink-0 w-6 h-6 rounded-full bg-#FFFBF1 flex items-center justify-center mt-1 transform transition-all group-hover:rotate-12">
                                <i class='bx bx-check text-18px' style="color:#FCAF17"></i>
                            </div>
                            <span class="text-gray-700  transition-colors">{{ benefit }}</span>
                        </div>
                    </div>
                </section>

                <!-- Course Content Section -->
                <section class="mt-12 md:mt-16">
                    <h2 class="text-2xl font-semibold text-gray-800 flex items-center justify-between">
                        Nội dung khoá học
                        <button @click="fullyExpanded"
                            class="text-#FCAF17 hover:text-yellow-400 text-sm flex items-center space-x-1">
                            <span>Mở rộng toàn bộ</span>
                        </button>
                    </h2>

                    <div class="my-6 space-y-4">
                        <div v-for="(module, index) in courseDetail?.courseModules" :key="`module-${index}`"
                            class="border border-gray-200 rounded-lg overflow-hidden module-container">
                            <div class="bg-gray-50 p-4 flex items-start flex-col md:(flex-row justify-between items-center) cursor-pointer hover:bg-gray-100 transition-colors"
                                @click="toggleModule(index)">
                                <div class="flex items-center space-x-2 font-medium">
                                    <div class="icon-container w-6 h-6 flex items-center justify-center overflow-hidden">
                                        <i :class="activeModules[index] ? 'bx bx-minus rotate-in' : 'bx bx-plus rotate-in'"
                                            class='text-24px transition-all duration-300' style='color:#FCAF17'></i>
                                    </div>
                                    <div>{{ index + 1 }}.</div>
                                    <h3 class="font-medium">{{ module.title }}</h3>
                                </div>

                                <div class="flex items-center space-x-2 ml-8 md:ml-0">
                                    <span class="text-sm text-gray-500">{{ module.lessons }} bài học</span>
                                </div>
                            </div>

                            <div :class="[
                                'module-content border-t border-gray-200 space-y-3 transition-all duration-500 ease-in-out',
                                activeModules[index] ? 'module-content-active' : 'module-content-inactive'
                            ]">
                                <div v-for="(lesson, lIndex) in module.content" :key="`lesson-${index}-${lIndex}`"
                                    class="flex items-start space-x-2 py-2 group lesson-item">
                                    <div
                                        class="flex-shrink-0 w-5 h-5 rounded-full bg-#FCAF17 flex items-center justify-center mt-1 transform transition-all group-hover:rotate-12">
                                        <i class='bx bx-check' style="color:#FFFFFF"></i>
                                    </div>
                                    <span class="text-gray-700  transition-colors">{{ lesson
                                    }}</span>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="self-stretch p-6 bg-#FAFAFA rounded-2xl flex flex-col justify-start items-center gap-10">
                        <div
                            class="self-stretch pb-4 border-b border-Border-Border-default flex flex-col justify-start items-start gap-4">
                            <div class="justify-start text-Text&Icon-Text-title text-2xl font-bold font-['Inter'] ">
                                Đánh giá </div>
                            <div class="flex justify-start items-center gap-8px">
                                <i class='bx bxs-star text-20px' style='color:#FF9100'></i>
                                <i class='bx bxs-star text-20px' style='color:#FF9100'></i>
                                <i class='bx bxs-star text-20px' style='color:#FF9100'></i>
                                <i class='bx bxs-star text-20px' style='color:#FF9100'></i>
                                <i class='bx bxs-star text-20px' style='color:#FF9100'></i>
                                <div class="flex justify-start items-center gap-4">
                                    <div class="justify-start text-#404040 text-xl font-bold font-['Inter'] leading-7">
                                        5 .0</div>
                                    <div
                                        class="justify-start text-#2A2A2A text-sm font-normal font-['Inter'] leading-tight">
                                        {{ courseDetail?.feedbacks.length }} lượt đánh giá</div>
                                </div>
                            </div>
                        </div>
                        <!-- Feedback items with transition group for smooth animation -->
                        <TransitionGroup name="feedback-list" tag="div" class="w-full feedback-container">
                            <div v-for="item in showFeedbacks" :key="item.name"
                                class="self-stretch flex flex-col justify-start items-start gap-6 feedback-item">
                                <div class="self-stretch inline-flex justify-start items-start gap-4">
                                    <div class="flex-1 flex justify-start items-center gap-4">
                                        <div
                                            class="w-16 h-16 relative rounded-33px shadow-[0px_4px_10px_0px_rgba(0,0,0,0.25)] border-[3px] border-white">
                                            <img :src="item.avatar" alt="Avatar"
                                                class="w-full h-full rounded-33px object-cover">
                                        </div>
                                        <div class="flex flex-col justify-start items-start gap-2">
                                            <div
                                                class="w-full h-6 justify-center text-18px font-bold font-['Inter'] leading-7">
                                                {{ item.name }}</div>
                                            <div class="inline-flex justify-start items-center gap-4px">
                                                <i class='bx bxs-star text-16px' style='color:#FF9100'></i>
                                                <i class='bx bxs-star text-16px' style='color:#FF9100'></i>
                                                <i class='bx bxs-star text-16px' style='color:#FF9100'></i>
                                                <i class='bx bxs-star text-16px' style='color:#FF9100'></i>
                                                <i class='bx bxs-star text-16px' style='color:#FF9100'></i>
                                            </div>
                                        </div>
                                    </div>
                                    <div
                                        class="justify-center text-Text&Icon-Text-label text-sm font-normal font-['Inter'] leading-tight">
                                        {{ item.date }}</div>
                                </div>
                                <div
                                    class="justify-center text-Text&Icon-Text-label text-base font-normal font-['Inter'] leading-normal">
                                    {{ item.comment }}</div>
                            </div>
                        </TransitionGroup>

                        <!-- Xem thêm button with animation -->
                        <div data-circle-button="No" data-left-icon="false" data-level="Primary" data-right-icon="true"
                            data-size="48px" data-status="Active" data-style="Text" data-text="Yes"
                            class="px-6 py-3 rounded-lg inline-flex justify-center items-center gap-2 show-more-button"
                            v-if="showFeedbacks.length < courseDetail?.feedbacks?.length">
                            <div @click="handleShowMore"
                                class="flex items-center cursor-pointer text-center justify-start text-#FCAF17 text-base font-medium font-['Inter'] hover:translate-y-1 leading-normal transition-all duration-300 "
                                :class="{ 'opacity-50 pointer-events-none': isAnimating, 'animate-pulse': isAnimating }">
                                Xem thêm <i class='bx bx-chevron-down text-20px transition-transform duration-300 '
                                    style='color:#FCAF17'></i> </div>
                            <div class="w-6 h-6 relative">
                                <div class="w-4 h-2 left-[4.25px] top-[7.75px] absolute bg-Primary-Primary"></div>
                            </div>
                        </div>
                    </div>
                </section>
            </div>

            <!-- Right Image & Course Details Section -->
            <div class="flex flex-col space-y-6 max-w-auto md:max-w-350px">
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
                                            <img src="../../public/thunder.png" alt="">
                                        </div>
                                        <div
                                            class="justify-start text-white text-xs font-medium font-['Inter'] leading-none tracking-tight">
                                            Ưu đãi đặc biệt</div>
                                    </div>
                                    <div class="inline-flex justify-start items-center gap-1.5">
                                        <div
                                            class="justify-start text-white text-xl font-medium font-['Inter'] leading-loose tracking-tight">
                                            {{ formatNumberWithDots(courseDetail?.promotions?.price * ((100 -
                                                courseDetail?.promotions?.percent) / 100)) }}đ
                                        </div>
                                    </div>
                                    <div class="inline-flex justify-start items-center gap-1">
                                        <div
                                            class="opacity-50 justify-start text-white text-xs font-medium font-['Inter'] line-through leading-none">
                                            {{ formatNumberWithDots(courseDetail?.promotions?.price) }}đ</div>
                                        <div
                                            class="px-1 py-0.5 bg-rose-50 rounded-md flex justify-center items-center gap-2.5">
                                            <div
                                                class="justify-start text-red-600 text-xs font-medium font-['Inter'] leading-none tracking-tight">
                                                -{{ courseDetail?.promotions?.percent }}%</div>
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
                                                {{ hours > 9 ? hours : `0${hours}` }} </div>
                                        </div>
                                        <div class="inline-flex flex-col justify-start items-start gap-1">
                                            <div class="w-1 h-1 bg-white rounded-3xl"></div>
                                            <div class="w-1 h-1 bg-white rounded-3xl"></div>
                                        </div>
                                        <div
                                            class="px-2.5 py-1 bg-white/30 rounded-lg flex justify-center items-end gap-2.5 overflow-hidden">
                                            <div
                                                class="justify-start text-white text-base font-medium font-['Inter'] leading-normal">
                                                {{ minutes > 9 ? minutes : `0${minutes}` }}</div>
                                        </div>
                                        <div class="inline-flex flex-col justify-start items-start gap-1">
                                            <div class="w-1 h-1 bg-white rounded-3xl"></div>
                                            <div class="w-1 h-1 bg-white rounded-3xl"></div>
                                        </div>
                                        <div
                                            class="px-2.5 py-1 bg-white/30 rounded-lg flex justify-center items-end gap-2.5 overflow-hidden">
                                            <div
                                                class="justify-start text-white text-base font-medium font-['Inter'] leading-normal">
                                                {{ seconds > 9 ? seconds : `0${seconds}` }}</div>
                                        </div>
                                    </div>
                                    <div class="self-stretch inline-flex justify-end items-center gap-2">
                                        <div
                                            class="justify-start text-white text-xs font-normal font-['Inter'] leading-none tracking-tight">
                                            {{ courseDetail?.promotions?.preOder }} người đã đặt</div>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <div class="mt-4 pt-4  space-y-3">
                            <h3 class="font-semibold text-xl">Khoá học Dropship</h3>

                            <div class="flex items-center space-x-2 text-gray-600">
                                <i class='bx bxs-book-bookmark'></i>
                                <span>Số buổi: {{ courseDetail?.promotions?.numberSessions }}</span>
                            </div>

                            <div class="flex items-center space-x-2 text-gray-600">
                                <i class='bx bxs-user'></i>
                                <span>Số lượng hs:
                                    {{ courseDetail?.promotions?.preOder }}/{{ courseDetail?.promotions?.limit }}</span>
                            </div>

                            <div class="flex items-center space-x-2 text-gray-600">
                                <i class='bx bxs-calendar'></i>
                                <span>Thời gian: {{ courseDetail?.promotions?.time }}</span>
                            </div>

                            <div class="flex items-center space-x-2 text-gray-600">
                                <i class='bx bxs-video'></i>
                                <span>Hình thức: {{ courseDetail?.promotions?.learningStyle }}</span>
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

.animate-fade-in {
    animation: fadeIn 0.8s ease-out forwards;
}

/* Icon rotation animations */
@keyframes rotateIn {
    0% {
        transform: rotate(-180deg);
        opacity: 0;
    }

    100% {
        transform: rotate(0);
        opacity: 1;
    }
}

.rotate-in {
    animation: rotateIn 0.3s ease-out forwards;
}

/* Module content animations */
.module-content {
    overflow: hidden;
}

.module-content-active {
    max-height: 1000px;
    padding: 1rem;
    opacity: 1;
}

.module-content-inactive {
    max-height: 0;
    padding-top: 0;
    padding-bottom: 0;
    opacity: 0;
}

/* Make the icon container maintain its size during animation */
.icon-container {
    position: relative;
}

/* Lesson item animations */
.lesson-item {
    transform: translateX(0);
    transition: transform 0.3s ease-out;
}

.lesson-item:hover {
    transform: translateX(5px);
}

/* Transitions for feedback items */
.feedback-list-enter-active {
    transition: all 0.6s ease-out;
}

.feedback-list-leave-active {
    transition: all 0.3s ease-in;
    position: absolute;
}

.feedback-list-enter-from {
    opacity: 0;
    transform: translateY(30px);
}

.feedback-list-leave-to {
    opacity: 0;
    transform: translateY(-30px);
}

.feedback-item {
    margin-bottom: 2rem;
    transition: all 0.4s ease;
    transform: scale(1);
}

.feedback-container {
    position: relative;
    width: 100%;
}

/* Show more button animations */
.show-more-button {
    transition: all 0.3s ease;
}

.show-more-button:hover {
    transform: translateY(-2px);
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

.animate-pulse {
    animation: pulse 1.5s infinite;
}
</style>