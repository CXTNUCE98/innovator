<script lang="ts" setup>
import { ref, computed, onMounted, onBeforeUnmount } from 'vue';

interface TestimonialItem {
    name: string;
    comment?: string;
    sessions?: string;
    avatar?: string;
    rate: number;
    img?: any;
}

// Base testimonial data
const baseCourses: TestimonialItem[] = [
    {
        name: 'Huy Đặng',
        comment: 'Khoá học rất hữu ích và dễ hiểu. Tôi đã học được rất nhiều kiến thức mới',
        avatar: 'https://dongvat.edu.vn/upload/2025/01/avatar-blackpink-mai-dinh-05.webp',
        rate: 5,
        img: null,
    },
    {
        name: 'Lam Giang',
        comment: 'Khoá học rất hữu ích và dễ hiểu. Tôi đã học được rất nhiều kiến thức mới',
        avatar: 'https://dongvat.edu.vn/upload/2025/01/avatar-blackpink-mai-dinh-05.webp',
        rate: 5,
        img: null,
    },
    {
        name: 'Mai Linh',
        comment: 'Khoá học rất hữu ích và dễ hiểu. Tôi đã học được rất nhiều kiến thức mới',
        avatar: 'https://dongvat.edu.vn/upload/2025/01/avatar-blackpink-mai-dinh-05.webp',
        rate: 5,
        img: null,
    },
    {
        name: 'Lisa',
        sessions: 'Khoá học rất hữu ích và dễ hiểu. Tôi đã học được rất nhiều kiến thức mới',
        avatar: 'https://dongvat.edu.vn/upload/2025/01/avatar-blackpink-mai-dinh-05.webp',
        rate: 5,
        img: null,
    },
];

// Responsive settings
const visibleCourses = ref(3);
const carouselRef = ref<HTMLElement | null>(null);
const navButtonsRef = ref<HTMLElement | null>(null);

// Autoplay controls
let autoplayInterval: number | null = null;
const isUserInteracting = ref(false);
const isAutoScrolling = ref(false);

// Start autoplay carousel
const startAutoplay = () => {
    if (isUserInteracting.value) return;

    stopAutoplay();
    autoplayInterval = window.setInterval(() => {
        autoNext();
    }, 4000); // Change duration if needed
};

// Stop autoplay
const stopAutoplay = () => {
    if (autoplayInterval) {
        clearInterval(autoplayInterval);
        autoplayInterval = null;
    }
};

// Update visible cards based on screen size
const updateVisibleCourses = () => {
    if (window.innerWidth < 768) {
        visibleCourses.value = 1;
    } else if (window.innerWidth < 1040) {
        visibleCourses.value = 2;
    } else {
        visibleCourses.value = 3;
    }
};

// Lifecycle hooks
onMounted(() => {
    updateVisibleCourses();
    window.addEventListener('resize', updateVisibleCourses);
    startAutoplay();

    window.addEventListener('blur', stopAutoplay);
    window.addEventListener('focus', () => {
        if (!isUserInteracting.value) {
            startAutoplay();
        }
    });
});

onBeforeUnmount(() => {
    window.removeEventListener('resize', updateVisibleCourses);
    stopAutoplay();
    window.removeEventListener('blur', stopAutoplay);
    window.removeEventListener('focus', () => {
        if (!isUserInteracting.value) {
            startAutoplay();
        }
    });
});

// Create extended course list for looping
const extendedCourses = computed(() => {
    return [
        ...baseCourses.slice(-visibleCourses.value),
        ...baseCourses,
        ...baseCourses.slice(0, visibleCourses.value),
    ];
});

// Carousel state
const currentIndex = ref(visibleCourses.value);
const isTransitioning = ref(true);
const isAnimating = ref(false);

// Auto next slide with loop
const autoNext = () => {
    if (!isTransitioning.value || isAnimating.value) return;

    isAutoScrolling.value = true;
    isAnimating.value = true;
    currentIndex.value++;
};

// Manual next, no loop
const next = () => {
    if (!isTransitioning.value || isAnimating.value) return;

    // Stop autoplay on manual navigation
    stopAutoplay();
    isUserInteracting.value = true;
    isAutoScrolling.value = false;

    // Check if at end
    const totalRealCourses = baseCourses.length;
    const maxIndex = visibleCourses.value + totalRealCourses - 1;

    if (currentIndex.value < maxIndex) {
        isAnimating.value = true;
        currentIndex.value++;
    }
};

// Manual prev, no loop
const prev = () => {
    if (!isTransitioning.value || isAnimating.value) return;

    // Stop autoplay on manual navigation
    stopAutoplay();
    isUserInteracting.value = true;
    isAutoScrolling.value = false;

    // Check if at start
    const minIndex = visibleCourses.value;

    if (currentIndex.value > minIndex) {
        isAnimating.value = true;
        currentIndex.value--;
    }
};

// Handle slide transition end
const handleTransitionEnd = () => {
    isTransitioning.value = false;
    isAnimating.value = false;

    const total = baseCourses.length;

    // Only perform looping when auto-scrolling
    if (isAutoScrolling.value) {
        if (currentIndex.value >= total + visibleCourses.value) {
            currentIndex.value = visibleCourses.value;
        }
        if (currentIndex.value < visibleCourses.value) {
            currentIndex.value = total + visibleCourses.value - 1;
        }
    }

    isAutoScrolling.value = false;

    requestAnimationFrame(() => {
        isTransitioning.value = true;
    });
};

// Button disabled state
const isPrevDisabled = computed(() => {
    return currentIndex.value <= visibleCourses.value || isAnimating.value;
});

const isNextDisabled = computed(() => {
    const totalRealCourses = baseCourses.length;
    const maxIndex = visibleCourses.value + totalRealCourses - 1;
    return currentIndex.value >= maxIndex || isAnimating.value;
});

// User interaction handlers
const handleMouseEnter = () => {
    isUserInteracting.value = true;
    stopAutoplay();
};

const handleMouseLeave = () => {
    isUserInteracting.value = false;
    startAutoplay();
};

const handleNavButtonFocus = () => {
    isUserInteracting.value = true;
    stopAutoplay();
};

const handleNavButtonBlur = (event: FocusEvent) => {
    // Check if focus moves outside navigation buttons
    if (
        !navButtonsRef.value?.contains(event.relatedTarget as Node) &&
        !carouselRef.value?.contains(event.relatedTarget as Node)
    ) {
        isUserInteracting.value = false;
        startAutoplay();
    }
};

const handleFocusIn = () => {
    isUserInteracting.value = true;
    stopAutoplay();
};

const handleFocusOut = (event: FocusEvent) => {
    // Check if focus moves outside carousel
    if (
        !carouselRef.value?.contains(event.relatedTarget as Node) &&
        !navButtonsRef.value?.contains(event.relatedTarget as Node)
    ) {
        isUserInteracting.value = false;
        startAutoplay();
    }
};
</script>

<template>
    <!-- <div class="w-full px-6 md:px-[10%] lg:px-[20%] py-[60px] md:py-[80px]"> -->
    <div class="max-w-6xl mx-auto mt-64px px-4 py-8 md:py-12">
        <div class="flex justify-between items-center mb-6">
            <h2 class="text-3xl font-semibold">Cảm nhận của học viên</h2>
            <div class="flex gap-2" ref="navButtonsRef" @focusin="handleNavButtonFocus" @focusout="handleNavButtonBlur">
                <button @click="prev" @focus="handleNavButtonFocus"
                    class="p-2 rounded-lg bg-gray-100 hover:bg-gray-200 disabled:opacity-50 disabled:cursor-not-allowed"
                    :disabled="isPrevDisabled">
                    <svg class="w-6 h-6 rotate-180" fill="currentColor" viewBox="0 0 20 20">
                        <path fill-rule="evenodd"
                            d="M7.293 14.707a1 1 0 010-1.414L11.586 9 7.293 4.707a1 1 0 011.414-1.414l5 5a1 1 0 010 1.414l-5 5a1 1 0 01-1.414 0z"
                            clip-rule="evenodd" />
                    </svg>
                </button>
                <button @click="next" @focus="handleNavButtonFocus"
                    class="p-2 rounded-lg bg-gray-100 hover:bg-gray-200 disabled:opacity-50 disabled:cursor-not-allowed"
                    :disabled="isNextDisabled">
                    <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 20 20">
                        <path fill-rule="evenodd"
                            d="M7.293 14.707a1 1 0 010-1.414L11.586 9 7.293 4.707a1 1 0 011.414-1.414l5 5a1 1 0 010 1.414l-5 5a1 1 0 01-1.414 0z"
                            clip-rule="evenodd" />
                    </svg>
                </button>
            </div>
        </div>

        <div class="overflow-hidden" ref="carouselRef" @mouseenter="handleMouseEnter" @mouseleave="handleMouseLeave"
            @focusin="handleFocusIn" @focusout="handleFocusOut">
            <div class="flex py-2 gap-6" :class="isTransitioning ? 'transition-transform duration-500 ease-in-out' : ''"
                :style="{
                    transform: `translateX(-${currentIndex * (100 / extendedCourses.length)}%)`,
                    width: `${(extendedCourses.length / visibleCourses) * 100}%`,
                }" @transitionend="handleTransitionEnd">
                <div v-for="(item, index) in extendedCourses" :key="index" class="box-border"
                    :style="{ width: `${100 / extendedCourses.length}%` }">
                    <div class="bg-neutral-50 rounded-2xl shadow-md p-6 flex flex-col gap-4 h-full">
                        <div class="flex items-center justify-between gap-4 mb-2">
                            <div class="flex gap-2">
                                <div
                                    class="w-16 h-16 relative bg-Background-Background-gray-3 rounded-[33px] shadow-[0px_4px_10px_0px_rgba(0,0,0,0.25)] border-[3px] border-white">
                                    <img v-if="item.avatar" :src="item.avatar" alt="Avatar"
                                        class="w-full h-full rounded-33px object-cover">
                                </div>
                                <div>
                                    <h3 class="text-lg font-bold">{{ item.name }}</h3>
                                    <div class="flex">
                                        <div v-for="star in 5" :key="star" class="text-yellow-400">
                                            <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 20 20">
                                                <path
                                                    d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z">
                                                </path>
                                            </svg>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <img src="../public/Symbol.png" alt="">
                        </div>
                        <p class="text-gray-700">
                            "{{ item.comment || item.sessions }}"
                        </p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
  
