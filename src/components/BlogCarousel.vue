<script lang="ts" setup>
import { ref, computed, onMounted, onBeforeUnmount } from 'vue';

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
const extendedBlogs = computed(() => {
    return [
        ...articles.value.slice(-visibleCourses.value),
        ...articles.value,
        ...articles.value.slice(0, visibleCourses.value),
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
    const totalRealCourses = articles.value?.length;
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

    const total = articles.value?.length;

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
    const totalRealCourses = articles.value?.length;
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

const router = useRouter()
function handleRedirect(id: string) {
    router.push(`/article/${id}`)
}
</script>

<template>
    <!-- <div class="w-full px-6 md:px-[10%] lg:px-[20%] py-[60px] md:py-[80px]"> -->
    <div class="max-w-6xl mx-auto px-0 md:px-4 py-4 md:py-12">
        <div class="flex justify-between items-center mb-6">
            <h2 class="text-3xl font-semibold">Xem thêm</h2>
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
            <div class="flex py-2 gap-2 md:gap-6" :class="isTransitioning ? 'transition-transform duration-500 ease-in-out' : ''"
                :style="{
                    transform: `translateX(-${currentIndex * (100 / extendedBlogs.length)}%)`,
                    width: `${(extendedBlogs.length / visibleCourses) * 100}%`,
                }" @transitionend="handleTransitionEnd">
                <div v-for="(item, index) in extendedBlogs" :key="index" class="box-border"
                    :style="{ width: `${100 / extendedBlogs.length}%` }">
                    <div class="bg-neutral-50 rounded-2xl shadow-md p-16px flex flex-col gap-4 h-full">
                        <img class="w-full h-180px object-cover rounded-lg" :src="item.image" alt="img">
                        <div class="w-fit bg-#DDF9FF text-#37C4E5 text-xs px-4 py-2 rounded-lg">{{
                            item.category }}</div>
                        <div @click="handleRedirect(item.id)" class="text-#2A2A2A text-18px font-500 cursor-pointer">
                            {{ item.title }}"
                        </div>
                        <div class="text-14px text-#7F7F7F">
                            {{ item.date }}
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
  
