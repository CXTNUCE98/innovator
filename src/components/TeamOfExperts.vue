<script setup lang="ts">
const team = [
    { name: 'Phùng Thế Kiên' },
    { name: 'Nguyễn Duy Tú' },
    { name: 'Tony Triệu' },
    { name: 'Tuấn KayO' },
    { name: 'Alex Trần' },
    { name: 'Thành Trung' },
];
</script>

<template>
    <div class="w-full px-6 md:px-10% lg:px-20% py-[60px] md:py-[80px]">
        <div class="mx-auto flex flex-col lg:flex-row items-start gap-10">
            <!-- Left content -->
            <div class="lg:w-1/3 ">
                <h2 class="text-2xl md:text-3xl font-bold text-gray-900 mb-4">Đội ngũ chuyên gia</h2>
                <p class="text-gray-600 mb-6">
                    Có kiến thức sâu rộng và kinh nghiệm thực tế, sẵn sàng chia sẻ cùng học viên trong quá trình học tập
                </p>
                <div
                    class=" bg-yellow-400 text-white px-5 py-2 rounded-lg shadow hover:bg-yellow-500 transition duration-300">
                    Xem tất cả
                </div>
                <div>Xem tất cả</div>
                <img src="../public/arrows_button.png" alt="">
            </div>

            <!-- Right team cards -->
            <div class="relative lg:w-2/3 grid grid-cols-2 sm:grid-cols-3 gap-6 p-4 rounded-lg">
                <div v-for="(member, index) in team" :key="index"
                    class="bg-white z-1 rounded-lg shadow p-4 flex flex-col items-center justify-center hover:shadow-md transition-shadow duration-300">
                    <!-- <div class="w-24 h-24 bg-gray-200 rounded-md mb-3 animate-pulse"></div> -->
                    <img class="w-full rounded-md"
                        src="https://img7.thuthuatphanmem.vn/uploads/2024/05/08/anh-avatar-gai-xinh-cuc-dep_044029122.png"
                        alt="">
                    <p class="text-sm text-center text-gray-800 font-medium">{{ member.name }}</p>
                </div>
                <div class="absolute bg-#FFFBF1 top-17% left-0 h-288px w-1024px "></div>
            </div>
        </div>
    </div>
</template>
<style scoped></style>