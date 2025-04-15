<script lang="ts" setup>

const isVisible = ref(false)
const sloganBox = ref(null)

onMounted(() => {
    // Trigger entrance animations after component is mounted
    setTimeout(() => {
        isVisible.value = true
    }, 100)

    // Optional: Animation for slogan box when scrolling
    if (window && 'IntersectionObserver' in window) {
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    isVisible.value = true
                    observer.disconnect()
                }
            })
        }, { threshold: 0.1 })

        if (sloganBox.value) {
            observer.observe(sloganBox.value)
        }
    }
})
</script>

<template>
    <section class="relative md:h-640px h-630px w-full overflow-hidden">
        <!-- Background Image with Overlay -->
        <div class="absolute inset-0 z-0">
            <div class="absolute inset-0 img-color "></div>
        </div>

        <!-- Content Container -->
        <div class="relative h-100% z-10 container flex justify-center items-center mx-auto px-4 py-16 md:py-24 lg:py-32">
            <div class="flex flex-col items-center justify-center text-center text-white ">
                <!-- Animated Slogan Box -->
                <div class="bg-white rounded-lg shadow-lg p-4 md:p-6 mb-6 transform transition-all duration-700 opacity-0 translate-y-8"
                    :class="{ 'opacity-100 translate-y-0': isVisible }" ref="sloganBox">
                    <div class="absolute top--8 left--7 z-11">
                        <svg xmlns="http://www.w3.org/2000/svg" width="39" height="43" viewBox="0 0 39 43" fill="none">
                            <path fill-rule="evenodd" clip-rule="evenodd"
                                d="M13.0489 40.1279C9.32492 39.0762 5.42609 38.5457 1.64397 38.0597C0.829355 37.9578 0.0730442 38.5264 0.0148577 39.3274C-0.101515 40.129 0.480691 40.8622 1.23712 40.9641C4.90286 41.4319 8.68465 41.9326 12.234 42.945C12.9904 43.1646 13.8054 42.7126 14.0381 41.9349C14.2709 41.1579 13.8053 40.348 13.0489 40.1279Z"
                                fill="white" />
                            <path fill-rule="evenodd" clip-rule="even odd"
                                d="M24.3365 25.2168C18.3433 19.0619 11.5937 13.6993 5.71685 7.3793C5.19318 6.78905 4.26219 6.75743 3.68033 7.30845C3.09846 7.86005 3.0405 8.78758 3.62237 9.37783C9.4992 15.716 16.2488 21.0961 22.242 27.2692C22.8239 27.8454 23.7547 27.8535 24.3365 27.2867C24.8602 26.7205 24.9184 25.793 24.3365 25.2168Z"
                                fill="white" />
                            <path fill-rule="evenodd" clip-rule="evenodd"
                                d="M35.5674 1.54341C35.742 5.06616 35.9162 8.58891 36.0907 12.1123C36.0907 12.9192 36.7893 13.5422 37.6039 13.503C38.4185 13.4631 39.0001 12.7763 39.0001 11.9688C38.8255 8.44018 38.6513 4.91216 38.4767 1.38413C38.4185 0.577224 37.7202 -0.0417174 36.9056 0.00219986C36.1492 0.0461172 35.5092 0.737085 35.5674 1.54341Z"
                                fill="white" />
                        </svg>
                    </div>
                    <h2 class="flex items-center justify-center gap-2 md:gap-4">
                        <span class="flex items-center gap-2">
                            <div class="bg-#FDFFEB p-2 rounded flex items-center justify-center">
                                <svg class="w-34px h-34px text-#B4CD26" fill="currentColor" viewBox="0 0 20 20">
                                    <path
                                        d="M11.3 1.046A1 1 0 0112 2v5h4a1 1 0 01.82 1.573l-7 10A1 1 0 018 18v-5H4a1 1 0 01-.82-1.573l7-10a1 1 0 011.12-.38z" />
                                </svg>
                            </div>
                            <span class="text-16px md:text-48px font-bold text-yellow-500">Innovate Today,</span>
                        </span>
                        <span class="text-16px md:text-48px font-bold text-gray-800">Grow Tomorrow</span>
                    </h2>
                </div>

                <!-- Main Heading -->
                <h1 class="text-24px md:text-32px lg:text-38px font-600 mb-10px transform transition-all duration-700 delay-300 opacity-0 translate-y-8"
                    :class="{ 'opacity-100 translate-y-0': isVisible }">
                    Định hình tương lai đổi mới kỹ thuật số
                </h1>

                <!-- Description -->
                <p class="text-20px px-4 md:(text-24px px-0) mb-10 transform transition-all duration-700 delay-500 opacity-0 translate-y-8"
                    :class="{ 'opacity-100 translate-y-0': isVisible }">
                    Hãy tham gia với chúng tôi trong hành trình học tập thú vị này và khám phá tiềm năng của bạn
                </p>

                <!-- CTA Button -->
                <button
                    class="bg-white text-20px text-gray-800 hover:bg-yellow-500 hover:text-white font-medium rounded-md px-10 py-3 transform transition-all duration-700 delay-700 opacity-0 translate-y-8"
                    :class="{ 'opacity-100 translate-y-0': isVisible }">
                    Đăng ký ngay
                </button>


            </div>
        </div>
    </section>
</template>
  

  
<style scoped>
.img-color {
    background: linear-gradient(0deg, rgba(252, 175, 23, 0.20) 0%, rgba(252, 175, 23, 0.20) 100%), linear-gradient(0deg, rgba(0, 0, 0, 0.20) 0%, rgba(0, 0, 0, 0.20) 100%), linear-gradient(0deg, rgba(0, 0, 0, 0.20) 0%, rgba(0, 0, 0, 0.20) 100%), url('@/public/hero_section.jpg') lightgray 50% / cover no-repeat;
}
</style>