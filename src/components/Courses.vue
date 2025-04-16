<script setup>
import { ref, computed, onMounted, onBeforeUnmount } from 'vue'
import Dropship from '@/public/course/dropship.png'
import Amazon from '@/public/course/amazon.png'
import Livestream from '@/public/course/livestream.png'
import Teamwork from '@/public/course/teamwork.png'

const baseCourses = [
    {
        name: 'Khóa học Dropship',
        sessions: 6,
        slot: 16,
        type: 'Cơ bản',
        rate: 5,
        img: Dropship,
    },
    {
        name: 'Khóa học Amazon',
        sessions: 6,
        slot: 16,
        type: 'Cơ bản',
        rate: 5,
        img: Amazon,
    },
    {
        name: 'Khóa học Livestream',
        sessions: 6,
        slot: 16,
        type: 'Nâng cao',
        rate: 5,
        img: Livestream,
    },
    {
        name: 'Khóa học Teamwork',
        sessions: 6,
        slot: 16,
        type: 'Cơ bản',
        rate: 5,
        img: Teamwork,
    },
]

const visibleCourses = ref(4)

let autoplayInterval = null

const startAutoplay = () => {
    autoplayInterval = setInterval(() => {
        next()
    }, 4000) // đổi số mili-giây nếu muốn nhanh/chậm hơn
}

const stopAutoplay = () => {
    if (autoplayInterval) clearInterval(autoplayInterval)
}

const updateVisibleCourses = () => {
    if (window.innerWidth < 768) {
        visibleCourses.value = 1
    } else if(window.innerWidth < 1040) {
        visibleCourses.value = 2
    }
    else if(window.innerWidth < 1400) {
        visibleCourses.value = 3
    } else {
        visibleCourses.value = 4
    }
}

onMounted(() => {
    updateVisibleCourses()
    window.addEventListener('resize', updateVisibleCourses)
})
onBeforeUnmount(() => {
    window.removeEventListener('resize', updateVisibleCourses)
})

// Clone phần tử đầu/cuối để tạo loop
const extendedCourses = computed(() => {
    return [
        ...baseCourses.slice(-visibleCourses.value),
        ...baseCourses,
        ...baseCourses.slice(0, visibleCourses.value),
    ]
})

const currentIndex = ref(visibleCourses.value)
const isTransitioning = ref(true)

const next = () => {
    if (!isTransitioning.value) return
    currentIndex.value++
}

const prev = () => {
    if (!isTransitioning.value) return
    currentIndex.value--
}

const handleTransitionEnd = () => {
    isTransitioning.value = false

    const total = baseCourses.length

    if (currentIndex.value >= total + visibleCourses.value) {
        currentIndex.value = visibleCourses.value
    }
    if (currentIndex.value < visibleCourses.value) {
        currentIndex.value = total + visibleCourses.value - 1
    }

    requestAnimationFrame(() => {
        isTransitioning.value = true
    })
}



onMounted(() => {
    startAutoplay()
    window.addEventListener('blur', stopAutoplay)
    window.addEventListener('focus', startAutoplay)
})

onBeforeUnmount(() => {
    stopAutoplay()
    window.removeEventListener('blur', stopAutoplay)
    window.removeEventListener('focus', startAutoplay)
})
</script>

<template>
    <div class="w-full px-6 md:px-10% lg:px-20% py-[60px] md:py-[80px]">
        <div class="flex justify-between items-center mb-6">
            <h2 class="text-4xl font-semibold">Khoá học</h2>
            <div class="flex gap-4">
                <button @click="prev" class="p-3 rounded-lg bg-gray-100 hover:bg-gray-200">
                    <svg class="w-6 h-6 rotate-180" fill="currentColor" viewBox="0 0 20 20">
                        <path fill-rule="evenodd"
                            d="M7.293 14.707a1 1 0 010-1.414L11.586 9 7.293 4.707a1 1 0 011.414-1.414l5 5a1 1 0 010 1.414l-5 5a1 1 0 01-1.414 0z"
                            clip-rule="evenodd" />
                    </svg>
                </button>
                <button @click="next" class="p-3 rounded-lg bg-gray-100 hover:bg-gray-200">
                    <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 20 20">
                        <path fill-rule="evenodd"
                            d="M7.293 14.707a1 1 0 010-1.414L11.586 9 7.293 4.707a1 1 0 011.414-1.414l5 5a1 1 0 010 1.414l-5 5a1 1 0 01-1.414 0z"
                            clip-rule="evenodd" />
                    </svg>
                </button>
            </div>
        </div>

        <div class="overflow-hidden">
            <div class="flex gap-24px" :class="isTransitioning ? 'transition-transform duration-500 ease-in-out' : ''" :style="{
                transform: `translateX(-${currentIndex * (100 / extendedCourses.length)}%)`,
                width: `${(extendedCourses.length / visibleCourses) * 100}%`,
            }" @transitionend="handleTransitionEnd">
                <div v-for="(item, index) in extendedCourses" :key="index" class="box-border "
                    :style="{ width: `${100 / extendedCourses.length}%` }">
                    <div class="bg-neutral-50 min-w-300px rounded-2xl shadow-md p-4 flex flex-col gap-4 h-full">
                        <div class="h-48 rounded-xl overflow-hidden">
                            <img :src="item.img" alt="" class="w-full h-full object-cover" />
                        </div>
                        <div class="text-lg font-semibold">{{ item.name }}</div>
                        <div class="flex gap-6 text-sm text-gray-600">
                            <div class="flex items-center gap-1"><i class="fa-solid fa-book"></i> {{ item.sessions }} buổi
                            </div>
                            <div class="flex items-center gap-1"><i class="fa-solid fa-user"></i> {{ item.slot }} chỗ</div>
                            <div class="flex items-center gap-1"><i class="fa-solid fa-trophy"></i> {{ item.type }}</div>
                        </div>
                        <div class="flex justify-between items-center">
                            <button class="px-4 py-2 bg-yellow-400 text-white rounded-lg text-sm hover:bg-yellow-500">
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