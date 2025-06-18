<script setup lang="ts">
import Dropship from "@/public/dropship_article.png"
import Amazon from "@/public/amazon_article.png"
import Livestream from "@/public/livestream_article.png"
import Teamwork from "@/public/teamwork_article.png"

const getArticles =  ref([...articles.value].sort(() => Math.random() - 0.5).slice(0, 4))


function getRandomItem(array) {
    // Kiểm tra mảng trống
    if (!array || array.length === 0) {
        return null;
    }

    // Tạo chỉ số ngẫu nhiên
    const randomIndex = Math.floor(Math.random() * array.length);

    // Trả về phần tử ở vị trí ngẫu nhiên
    return array[randomIndex];
}

const outstanding = getRandomItem(getArticles.value)
const articleFeatures = getRemainingItems(getArticles.value, outstanding)

function getRemainingItems(array, selectedItem) {
    // Kiểm tra mảng trống
    if (!array || array.length === 0) {
        return [];
    }

    // Lọc các phần tử khác với phần tử đã chọn
    return array.filter(item => item !== selectedItem);
}


const hoveredArticle = ref<string | null>(null);

// Animation for articles when they come into view
onMounted(() => {
    if (process.client) {
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('animate-fadeIn');
                    observer.unobserve(entry.target);
                }
            });
        }, {
            threshold: 0.1
        });

        document.querySelectorAll('.featured-article, .article-card').forEach(article => {
            observer.observe(article);
        });
    }
});

const router = useRouter()
function goToDetailArticle(id: string) {
    router.push(`/article/${id}`)
}
</script>

<template>
    <!-- <div class="w-full px-6 md:px-[10%] lg:px-[20%] py-[60px] md:py-[80px]"> -->
    <div class="max-w-6xl mx-auto mt-64px px-4 py-8 md:py-12">
        <div class="container mx-auto max-w-6xl">
            <header class="mb-8">
                <div class="flex flex-wrap justify-between">
                    <h1 class="text-3xl font-bold text-gray-800">Bài viết nổi bật</h1>
                    <button
                        class="bg-gray-100 hover:bg-gray-200 text-gray-800 px-4 py-2 rounded-md transition-colors duration-300">
                        Xem tất cả
                    </button>
                </div>
                <p class="text-gray-600 mt-1">Tổng hợp các bài viết chia sẻ về kinh nghiệm miễn phí và các tin tức sự
                    kiện
                </p>
            </header>

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                <!-- Featured Article -->
                <div class="featured-article bg-white rounded-lg overflow-hidden transform transition-transform duration-300"
                    @mouseover="hoveredArticle = 'dropship'" @mouseleave="hoveredArticle = null">
                    <div class="relative h-56 md:h-64">
                        <img :src="outstanding.image" alt="Featured Article" class="w-full h-full rounded-16px object-cover">
                        <div class="absolute inset-0 bg-gradient-to-t rounded-16px from-black/50 to-transparent"></div>
                    </div>
                    <div>
                        <h2 @click="goToDetailArticle(outstanding.id)" class="text-16px font-bold py-3 cursor-pointer">{{ outstanding.title }}
                        </h2>
                        <span
                            class="inline-block bg-blue-100 text-blue-500 px-3 py-1 text-xs rounded-full font-medium mb-3">Dropship</span>
                        <p class="text-gray-600 text-14px mb-4">{{ outstanding.des }}</p>
                        <div class="text-gray-500 text-sm">{{ outstanding.date }}</div>
                    </div>
                </div>

                <!-- Right Column Articles -->
                <div class="space-y-6">
                    <!-- Article Items -->
                    <template v-for="item in articleFeatures" :key="item.title">
                        <div class="article-card flex flex-col md:flex-row gap-4 bg-white rounded-lg overflow-hidden transform transition-transform duration-300 hover:-translate-y-1"
                            @mouseover="hoveredArticle = item.title" @mouseleave="hoveredArticle = null">
                            <div class="md:w-2/5 h-40 overflow-hidden">
                                <img :src="item.image" alt="Article image" class="w-full h-full object-cover rounded-12px">
                            </div>
                            <div class="flex-1">
                                <div class="flex flex-col justify-between items-start mb-1">
                                    <h3 @click="goToDetailArticle(item.id)" class="text-16px font-bold cursor-pointer">{{ item.title }}</h3>
                                    <span
                                        class="inline-block bg-blue-100 text-blue-500 px-2 py-1 text-xs rounded-full font-medium mt-2">Dropship</span>
                                </div>
                                <p class="text-gray-600 text-12px mb-3">{{ item.des }}</p>
                                <div class="text-gray-500 text-xs">{{ item.date }}</div>
                            </div>
                        </div>
                    </template>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
body {
    background-color: #f7f9fc;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.container {
    animation: fadeIn 0.5s ease-in-out;
}

/* Fix for image consistency */
img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;
}

.featured-article img {
    height: 100%;
}

@keyframes fadeIn {
    from {
        opacity: 0;
        transform: translateY(10px);
    }

    to {
        opacity: 1;
        transform: translateY(0);
    }
}

.animate-fadeIn {
    animation: slideUp 0.6s ease-out forwards;
}

@keyframes slideUp {
    from {
        opacity: 0;
        transform: translateY(20px);
    }

    to {
        opacity: 1;
        transform: translateY(0);
    }
}

.read-more-btn:hover svg {
    transform: translateX(2px);
}

/* For the featured article image gradient overlay */
.featured-article:hover .absolute {
    background: linear-gradient(to top, rgba(0, 0, 0, 0.7), transparent);
}
</style>