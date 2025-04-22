<script setup lang="ts">
import { ref, computed, onMounted, onBeforeUnmount } from 'vue'
import Dropship from '@/public/course/dropship.png'
import Amazon from '@/public/course/amazon.png'
import Livestream from '@/public/course/livestream.png'
import Teamwork from '@/public/course/teamwork.png'

const baseCourses = [
    {
        id: 'abc-b465-v21gh-1',
        name: 'Khóa học Dropship',
        sessions: 6,
        slot: 16,
        type: 'Cơ bản',
        rate: 5,
        img: Dropship,        
    },
    {
        id: 'abc-b465-v21gh-2',
        name: 'Content Creator',
        sessions: 6,
        slot: 16,
        type: 'Cơ bản',
        rate: 5,
        img: Amazon,
    },
    {
        id: 'abc-b465-v21gh-3',
        name: 'Khoá học Affiliate Marketing',
        sessions: 6,
        slot: 16,
        type: 'Nâng cao',
        rate: 5,
        img: Livestream,
    },
    {
        id: 'abc-b465-v21gh-4',
        name: 'Khoá học Digital Marketing',
        sessions: 6,
        slot: 16,
        type: 'Cơ bản',
        rate: 5,
        img: Teamwork,
    },
    {
        id: 'abc-b465-v21gh-5',
        name: 'Khoá học Kinh doanh Online',
        sessions: 6,
        slot: 16,
        type: 'Cơ bản',
        rate: 5,
        img: Teamwork,
    },
    {
        id: 'abc-b465-v21gh-6',
        name: 'Khoá học Quản lý tài chính cá nhân',
        sessions: 6,
        slot: 16,
        type: 'Cơ bản',
        rate: 5,
        img: Teamwork,
    },
    {
        id: 'abc-b465-v21gh-7',
        name: 'Khoá học Thiết kế đồ họa',
        sessions: 6,
        slot: 16,
        type: 'Cơ bản',
        rate: 5,
        img: Teamwork,
    },
    {
        id: 'abc-b465-v21gh-8',
        name: 'Khoá học Quản lý thời gian',
        sessions: 6,
        slot: 16,
        type: 'Cơ bản',
        rate: 5,
        img: Teamwork,
    },
    {
        id: 'abc-b465-v21gh-9',
        name: 'Khoá học Kỹ năng bán hàng',
        sessions: 6,
        slot: 16,
        type: 'Cơ bản',
        rate: 5,
        img: Teamwork,
    },
    {
        id: 'abc-b465-v21gh-10',
        name: 'Khoá học Amazon FBA',
        sessions: 6,
        slot: 16,
        type: 'Cơ bản',
        rate: 5,
        img: Teamwork,
    },
    {
        id: 'abc-b465-v21gh-11',
        name: 'Khoá học Livestream bán hàng',
        sessions: 6,
        slot: 16,
        type: 'Cơ bản',
        rate: 5,
        img: Teamwork,
    },
]

const visibleCourses = ref(4)
const carouselRef = ref(null)
const navButtonsRef = ref(null)

let autoplayInterval = null
const isUserInteracting = ref(false)
const isAutoScrolling = ref(false)

const startAutoplay = () => {
    if (isUserInteracting.value) return

    stopAutoplay()
    autoplayInterval = setInterval(() => {
        autoNext()
    }, 4000) // đổi số mili-giây nếu muốn nhanh/chậm hơn
}

const stopAutoplay = () => {
    if (autoplayInterval) {
        clearInterval(autoplayInterval)
        autoplayInterval = null
    }
}

const updateVisibleCourses = () => {
    if (window.innerWidth < 768) {
        visibleCourses.value = 1
    } else if (window.innerWidth < 1040) {
        visibleCourses.value = 2
    }
    else if (window.innerWidth < 1400) {
        visibleCourses.value = 3
    } else {
        visibleCourses.value = 4
    }
}

onMounted(() => {
    updateVisibleCourses()
    window.addEventListener('resize', updateVisibleCourses)
    startAutoplay()
})

onBeforeUnmount(() => {
    window.removeEventListener('resize', updateVisibleCourses)
    stopAutoplay()
})

// Clone phần tử đầu/cuối để tạo loop cho auto-scroll
const extendedCourses = computed(() => {
    return [
        ...baseCourses.slice(-visibleCourses.value),
        ...baseCourses,
        ...baseCourses.slice(0, visibleCourses.value),
    ]
})

const currentIndex = ref(visibleCourses.value)
const isTransitioning = ref(true)
const isAnimating = ref(false)

// Auto scroll với loop
const autoNext = () => {
    if (!isTransitioning.value || isAnimating.value) return

    isAutoScrolling.value = true
    isAnimating.value = true
    currentIndex.value++
}

// Manual next không loop
const next = () => {
    if (!isTransitioning.value || isAnimating.value) return

    // Stop autoplay on manual navigation
    stopAutoplay()
    isUserInteracting.value = true
    isAutoScrolling.value = false

    // Kiểm tra nếu đã đến course cuối
    const totalRealCourses = baseCourses.length
    const maxIndex = visibleCourses.value + totalRealCourses - 1

    if (currentIndex.value < maxIndex) {
        isAnimating.value = true
        currentIndex.value++
    }
}

// Manual prev không loop
const prev = () => {
    if (!isTransitioning.value || isAnimating.value) return

    // Stop autoplay on manual navigation
    stopAutoplay()
    isUserInteracting.value = true
    isAutoScrolling.value = false

    // Kiểm tra nếu đã đến course đầu
    const minIndex = visibleCourses.value

    if (currentIndex.value > minIndex) {
        isAnimating.value = true
        currentIndex.value--
    }
}

const handleTransitionEnd = () => {
    isTransitioning.value = false
    isAnimating.value = false

    const total = baseCourses.length

    // Chỉ thực hiện loop khi auto-scroll
    if (isAutoScrolling.value) {
        if (currentIndex.value >= total + visibleCourses.value) {
            currentIndex.value = visibleCourses.value
        }
        if (currentIndex.value < visibleCourses.value) {
            currentIndex.value = total + visibleCourses.value - 1
        }
    }

    isAutoScrolling.value = false

    requestAnimationFrame(() => {
        isTransitioning.value = true
    })
}

// Kiểm tra nút prev/next có bị disabled hay không
const isPrevDisabled = computed(() => {
    return currentIndex.value <= visibleCourses.value || isAnimating.value
})

const isNextDisabled = computed(() => {
    const totalRealCourses = baseCourses.length
    const maxIndex = visibleCourses.value + totalRealCourses - 1
    return currentIndex.value >= maxIndex || isAnimating.value
})

const handleMouseEnter = () => {
    isUserInteracting.value = true
    stopAutoplay()
}

const handleMouseLeave = () => {
    isUserInteracting.value = false
    startAutoplay()
}

const handleNavButtonFocus = () => {
    isUserInteracting.value = true
    stopAutoplay()
}

const handleNavButtonBlur = (event) => {
    // Kiểm tra xem focus có chuyển ra ngoài navigation buttons không
    if (!navButtonsRef.value?.contains(event.relatedTarget) &&
        !carouselRef.value?.contains(event.relatedTarget)) {
        isUserInteracting.value = false
        startAutoplay()
    }
}

const handleFocusIn = () => {
    isUserInteracting.value = true
    stopAutoplay()
}

const handleFocusOut = (event) => {
    // Kiểm tra xem focus có chuyển ra ngoài carousel không
    if (!carouselRef.value?.contains(event.relatedTarget) &&
        !navButtonsRef.value?.contains(event.relatedTarget)) {
        isUserInteracting.value = false
        startAutoplay()
    }
}

onMounted(() => {
    window.addEventListener('blur', stopAutoplay)
    window.addEventListener('focus', () => {
        if (!isUserInteracting.value) {
            startAutoplay()
        }
    })
})

onBeforeUnmount(() => {
    stopAutoplay()
    window.removeEventListener('blur', stopAutoplay)
    window.removeEventListener('focus', startAutoplay)
})

const router = useRouter()

function goToCourseDetail(id: string) {
    router.push(`/course/${id}`)
}
</script>

<template>
    <!-- <div class="w-full px-6 md:px-10% lg:px-20% py-[60px] md:py-[80px]"> -->
    <div class="max-w-6xl mx-auto mt-64px px-4 py-8 md:py-12">
        <div class="flex justify-between items-center mb-6">
            <h2 class="text-4xl font-semibold">Khoá học</h2>
            <div class="flex gap-4" ref="navButtonsRef" @focusin="handleNavButtonFocus" @focusout="handleNavButtonBlur">
                <button @click="prev" @focus="handleNavButtonFocus"
                    class="p-3 rounded-lg bg-gray-100 hover:bg-gray-200 disabled:opacity-50 disabled:cursor-not-allowed"
                    :disabled="isPrevDisabled">
                    <svg class="w-6 h-6 rotate-180" fill="currentColor" viewBox="0 0 20 20">
                        <path fill-rule="evenodd"
                            d="M7.293 14.707a1 1 0 010-1.414L11.586 9 7.293 4.707a1 1 0 011.414-1.414l5 5a1 1 0 010 1.414l-5 5a1 1 0 01-1.414 0z"
                            clip-rule="evenodd" />
                    </svg>
                </button>
                <button @click="next" @focus="handleNavButtonFocus"
                    class="p-3 rounded-lg bg-gray-100 hover:bg-gray-200 disabled:opacity-50 disabled:cursor-not-allowed"
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
            <div class="flex py-2 gap-24px" :class="isTransitioning ? 'transition-transform duration-500 ease-in-out' : ''"
                :style="{
                    transform: `translateX(-${currentIndex * (100 / extendedCourses.length)}%)`,
                    width: `${(extendedCourses.length / visibleCourses) * 100}%`,
                }" @transitionend="handleTransitionEnd">
                <div v-for="(item, index) in extendedCourses" :key="index" class="box-border"
                    :style="{ width: `${100 / extendedCourses.length}%`, minWidth: '250px' }">
                    <div class="bg-neutral-50 rounded-2xl shadow-md p-4 flex flex-col gap-4 h-full">
                        <div class="h-48 rounded-xl overflow-hidden">
                            <img :src="item.img" alt="" class="w-full h-full object-cover" />
                        </div>
                        <div @click="goToCourseDetail(item.id)" class="text-16px font-semibold cursor-pointer h-48px">{{ item.name }}</div>
                        <div class="flex flex-wrap gap-2 sm:gap-4 text-13px text-gray-600">
                            <div class="flex items-center gap-1"><i class="fa-solid fa-book"></i> {{ item.sessions }} buổi
                            </div>
                            <div class="flex items-center gap-1"><i class="fa-solid fa-user"></i> {{ item.slot }} chỗ</div>
                            <div class="flex items-center gap-1"><i class="fa-solid fa-trophy"></i> {{ item.type }}</div>
                        </div>
                        <div class="flex justify-between items-center">
                            <button class="px-4 py-2 bg-yellow-400 text-white rounded-lg text-sm hover:bg-yellow-500"
                                @focus="handleFocusIn">
                                Đăng ký
                            </button>
                            <div class="relative w-10 h-10">
                                <div class="absolute w-10 h-10 rounded-full border-2 border-gray-200"></div>
                                <div
                                    class="absolute w-10 h-10 origin-top-left rotate-[30deg] border-2 border-orange-300 rounded-full left-[12.68px] -top-[7.32px]">
                                </div>
                                <div
                                    class="absolute w-10 h-10 origin-top-left -rotate-90 border-2 border-orange-300 rounded-full top-[40px]">
                                </div>
                                <div class="absolute w-8 h-8 bg-white rounded-full left-[3px] top-[3px] z-10"></div>
                                <div class="absolute left-[15px] top-[8px] text-black text-base font-medium z-20">5</div>
                                <div class="absolute left-[31px] top-[8px] text-amber-500 text-xs font-black z-20">
                                    <i class="fa-solid fa-star"></i>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>