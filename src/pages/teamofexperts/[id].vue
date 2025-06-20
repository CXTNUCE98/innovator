<script setup lang="ts">
const route = useRoute()
const idExpert = computed(() => {
    return route?.params?.id as string
})

const expertDetail = ref(teamOfExperts.value?.find((el) => el.id === idExpert.value))
const router = useRouter()
function onGoBack() {
    router.back()
}
</script>

<template>
    <div class="max-w-6xl mx-auto mt-64px px-4 py-8 md:py-12">
        <div @click="onGoBack" class="hidden md:block pb-32px">
            <i class='bx bx-arrow-back rounded-full bg-#F5F5F5 p-2 text-20px cursor-pointer'></i>
        </div>
        <div class="flex flex-wrap gap-64px justify-center">
            <div>
                <img :src="expertDetail.img" alt="img" class="w-full max-h-400px rounded-16px h-full object-cover">
            </div>
            <div class="text-#555555">
                <div class="text-#2A2A2A text-36px font-bold">
                    {{ expertDetail.name }}
                </div>
                <div class="pb-40px">
                    {{ expertDetail.duty }}
                </div>
                <div v-for="(item, index) in expertDetail.experience" :key="index">
                    <div>{{ item }}</div>
                </div>

                <div class="flex gap-2 items-center pt-40px pb-4">
                    <div class="flex justify-center items-center rounded-full bg-#FFFBF1 w-12 h-12">
                        <i class='bx bx-envelope text-#FCAF17 text-20px'></i>
                    </div>
                    <p>{{ expertDetail.email }}</p>
                </div>
                <div class="flex items-center gap-2">
                    <div class="flex justify-center items-center rounded-full bg-#FFFBF1 w-12 h-12">
                        <i class='bx bx-phone text-#FCAF17 text-20px' ></i>
                    </div>
                    <p>{{ expertDetail.phone }}</p>
                </div>
            </div>
        </div>

        <!-- Related Articles Section -->
        <section class="mb-6 animate-fadeIn">
            <ExpertCarousel />            
        </section>
    </div>
</template>
<style scoped>

</style>