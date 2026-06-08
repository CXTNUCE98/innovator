<script setup lang="ts">

const router = useRouter()
function handleRedirect(id: string) {
    router.push(`/teamofexperts/${id}`)
}
function goToExpertsPage() {
    router.push('/teamofexperts/')
}
</script>

<template>
    <div class="w-full px-4 md:px-12 lg:px-[200px] py-12 lg:py-[100px] overflow-hidden md:overflow-visible">
        <div class="flex flex-col lg:flex-row items-center gap-10 lg:gap-[100px]">
            <!-- Left content -->
            <div class="lg:w-[409px] shrink-0">
                <h2 class="text-2xl md:text-36px font-bold text-gray-900 mb-4">Đội ngũ chuyên gia</h2>
                <p class="text-gray-600 mb-6 text-base leading-relaxed">
                    Có kiến thức sâu rộng và kinh nghiệm thực tế, sẵn sàng chia sẻ cùng học viên trong quá trình học tập
                </p>
                <div class="flex gap-3 items-center">
                    <div @click="goToExpertsPage"
                        class="cursor-pointer bg-#FCAF17 text-white px-6 py-3 rounded-lg shadow hover:bg-yellow-500 transition duration-300 font-medium">
                        Xem tất cả
                    </div>
                    <img src="../public/arrows_button.png" alt="">
                </div>
            </div>

            <!-- Right team cards -->
            <div class="relative flex-1 min-w-0">
                <!-- Decorative background -->
                <div class="absolute inset-y--8 -right-[200px] left-0 bg-#FFFBF1 rounded-l-[40px]"></div>
                <!-- Cards grid -->
                <div class="relative z-10 grid grid-cols-2 sm:grid-cols-3 gap-4 py-8 px-4">
                    <div v-for="(member, index) in teamOfExperts" :key="index"
                        class="bg-white rounded-xl shadow p-3 cursor-pointer flex flex-col items-center hover:shadow-md transition-shadow duration-300"
                        @click="handleRedirect(member.id)">
                        <img class="w-full aspect-square object-cover rounded-lg mb-2"
                            :src="member.img" :alt="member.name">
                        <p class="text-sm text-center text-gray-800 font-medium">{{ member.name }}</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped></style>