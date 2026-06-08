<script setup>

const isVisible = ref(false);

onMounted(() => {
    setTimeout(() => {
        isVisible.value = true;
    }, 300);
});

</script>

<template>
    <main class="min-h-screen bg-white flex flex-col items-center gap-20">
        <HeroSection />
        <Distributor />

        <!-- Start your business journey today -->
        <div class="w-full px-4 md:px-12 lg:px-[200px]">
            <div class="flex flex-col lg:flex-row items-center gap-8 lg:gap-16">
                <!-- Text content -->
                <div class="w-full lg:w-1/2 flex flex-col gap-8 md:gap-13 transition-all duration-1000 transform"
                    :class="isVisible ? 'opacity-100 translate-x-0' : 'opacity-0 -translate-x-12'">
                    <h2>
                        <span class="text-24px md:text-48px font-bold font-['Nunito_Sans'] leading-tight text-gray-900">Khởi đầu hành trình kinh doanh </span>
                        <span class="text-24px md:text-48px font-bold font-['Nunito_Sans'] leading-tight text-#FCAF17">ngay hôm nay</span>
                    </h2>
                    <p class="text-base md:text-lg font-normal leading-relaxed text-#555555 max-w-[730px]">
                        Tại Innovator Academy, chúng tôi cam kết mang đến những khóa học chất lượng và thực tiễn
                        trong lĩnh vực. Với đội ngũ giảng viên giàu kinh nghiệm và phương pháp giảng dạy hiện đại, chúng
                        tôi đã giúp hàng ngàn học viên đạt được thành công vượt bậc trong sự nghiệp.
                    </p>
                    <a href="#" class="text-gray-500 text-lg md:text-22px font-normal underline hover:text-yellow-500 transition-colors cursor-pointer">
                        Tìm hiểu thêm
                    </a>
                </div>

                <!-- Video container -->
                <div class="w-full lg:w-1/2 relative transition-all duration-1000 transform"
                    :class="isVisible ? 'opacity-100 translate-x-0' : 'opacity-0 translate-x-12'">
                    <div class="relative">
                        <!-- Decorative rectangles -->
                        <div class="absolute hidden md:block bottom-0 right-0 bg-#FBC456 w-[231px] h-[231px] rounded-2xl translate-x-4 translate-y-4"></div>
                        <div class="absolute hidden md:block top-0 left-0 bg-#FBC456 w-[138px] h-[138px] rounded-2xl -translate-x-4 -translate-y-4"></div>
                        <!-- Video -->
                        <div class="relative z-10 p-5">
                            <iframe
                                class="w-full aspect-video rounded-2xl shadow-lg"
                                src="https://www.youtube.com/embed/Wb06kwt_f9U?si=8CkW5YaNSysQ5NQz&autoplay=1"
                                title="YouTube video player" frameborder="0"
                                allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
                                allowfullscreen>
                            </iframe>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Course -->
        <Courses />

        <!-- Team of experts -->
        <TeamOfExperts />

        <!-- Training method -->
        <TrainingMethod />

        <!-- Student feedback -->
        <StudentFeedback />

        <!-- Featured Articles -->
        <FeaturedArticles />

        <!-- FAQ -->
        <FAQ />
    </main>
</template>

<style scoped>
</style>