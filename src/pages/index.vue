<script setup>
import Dropship from "@/public/course/dropship.png"
import Amazon from "@/public/course/amazon.png"
import Livestream from "@/public/course/livestream.png"
import Teamwork from "@/public/course/teamwork.png"

const isVisible = ref(false);

const courses = [
    {
        name: 'Khóa học Dropship',
        sessions: 6,
        slot: 16,
        type: 'Cơ bản',
        rate: 5,
        link: '1',
        img: Dropship,
    },
    {
        name: 'Khóa học Amazon',
        sessions: 6,
        slot: 16,
        type: 'Cơ bản',
        rate: 5,
        link: '1',
        img: Amazon,
    },
    {
        name: 'Khóa học Livestream',
        sessions: 6,
        slot: 16,
        type: 'Nâng cao',
        rate: 5,
        link: '1',
        img: Livestream,
    },
    {
        name: 'Khóa học Teamwork',
        sessions: 6,
        slot: 16,
        type: 'Cơ bản',
        rate: 5,
        link: '1',
        img: Teamwork,
    },
]

onMounted(() => {
    // Kích hoạt animation khi component được mount
    setTimeout(() => {
        isVisible.value = true;
    }, 300);
});


</script>

<template>
    <main class="min-h-screen bg-white">
        <HeroSection />
        <Distributor />

        <!-- Start your business journey today -->
        <div class="flex justify-center px-4 md:px-10% lg:px-20%">
            <div class="py-16 md:py-16 lg:py-80px w-full">
                <div class="flex flex-col lg:flex-row gap-8 md:gap-12 lg:gap-16">
                    <!-- Text content -->
                    <div class="w-full lg:w-1/2 flex flex-col justify-start items-start gap-4 md:gap-6 transition-all duration-1000 transform"
                        :class="isVisible ? 'opacity-100 translate-x-0' : 'opacity-0 -translate-x-12'">
                        <div class=" justify-start"><span
                                class="text-Text&Icon-Text-title text-24px md:text-4xl font-bold font-['Inter'] leading-32px md:leading-[57.60px]">Khởi
                                đầu hành trình kinh doanh </span><span
                                class="text-Primary-Primary text-24px md:text-4xl font-bold font-['Inter'] leading-32px md:leading-[57.60px] text-#FCAF17">ngay
                                hôm
                                nay</span></div>
                        <div
                            class="justify-start text-Text&Icon-Text-body text-base font-normal font-['Inter'] leading-24px md:(leading-9 text-xl) tracking-tight text-#555555">
                            Tại Innovator Academy, chúng tôi cam kết mang đến những khóa học chất lượng và thực tiễn trong
                            lĩnh vực. Với đội ngũ giảng viên giàu kinh nghiệm và phương pháp giảng dạy hiện đại, chúng tôi
                            đã giúp hàng ngàn học viên đạt được thành công vượt bậc trong sự nghiệp.
                        </div>
                        <div
                            class="justify-start text-gray-500 text-lg md:text-22px font-normal font-['Inter'] underline hover:text-yellow-500 transition-colors cursor-pointer">
                            Tìm hiểu thêm
                        </div>
                    </div>

                    <!-- Video container -->
                    <div class="w-full lg:w-1/2 relative aspect-video lg:aspect-auto transition-all duration-1000 transform"
                        :class="isVisible ? 'opacity-100 translate-x-0' : 'opacity-0 translate-x-12'">
                        <div
                            class="absolute md:block hidden top-0 left-0 bg-#FBC456 w-16 h-16 md:w-24 md:h-24 lg:w-32 lg:h-32 rounded-lg transform -translate-x-4 -translate-y-4 animate-pulse">
                        </div>
                        <div
                            class="absolute md:block hidden bottom-0 right-0 bg-#FBC456 w-24 h-24 md:w-32 md:h-32 lg:w-48 lg:h-48 rounded-lg transform translate-x-4 translate-y-4 animate-pulse">
                        </div>

                        <div class="absolute inset-0 p-0 md:p-5">
                            <iframe class="w-full h-full rounded-lg object-cover shadow-lg transform transition-transform"
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
        
        <!-- Trainning method -->
         <TrainingMethod />

         <!-- Student feedback -->
          <StudentFeedback />

          <!-- Featured Articles -->
           <FeaturedArticles />
    </main>
</template>

<style scoped>
@keyframes pulse {

    0%,
    100% {
        opacity: 1;
        transform: scale(1);
    }

    50% {
        opacity: 1;
        transform: scale(1.05);
    }
}

.animate-pulse {
    animation: pulse 3s infinite ease-in-out;
}
</style>