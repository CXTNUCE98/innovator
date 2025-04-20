<script setup lang="ts">
import Dropship from "@/public/dropship_article.png"
import Amazon from "@/public/amazon_article.png"
import Livestream from "@/public/livestream_article.png"
import Teamwork from "@/public/teamwork_article.png"

const articles = [
    {
        title: 'Bí Quyết Thành Công Với Dropship: Khám Phá Chiến Lược Đỉnh Cao',
        des: 'Bạn đang muốn khởi nghiệp với mô hình dropship nhưng chưa biết bắt đầu từ đâu? Hãy cùng chúng tôi khám phá những chiến lược đỉnh cao để xây dựng một cửa hàng dropship thành công. Khóa học của chúng tôi sẽ trang bị cho bạn kiến thức từ cơ bản đến nâng cao, giúp bạn tự tin trên con đường kinh doanh trực tuyến.',
        img: Dropship,
        date: '24/06/2024'
    },
    {
        title: 'Làm Chủ Sàn Amazon: Từ Người Mới Đến Chuyên Gia',
        des: 'Amazon là một thị trường tiềm năng nhưng cũng đầy thách thức. Để trở thành người bán hàng thành công trên Amazon sử dụng công cụ quảng cáo hiệu quả.',
        img: 'https://dddn.1cdn.vn/thumbs/1200x630/2021/07/08/diendandoanhnghiep.vn-media-uploaded-502-2021-07-07-_jeffbezos1.jpg',
        date: '24/06/2024'
    },
    {
        title: 'Livestream Bán Hàng: Nghệ Thuật Tăng Doanh Số Tức Thì',
        des: 'Livestream bán hàng đang trở thành xu hướng hot giúp tăng doanh số một cách nhanh chóng. Những ảnh hưởng nào để thực hiện một buổi livestream thành công?',
        img: Livestream,
        date: '24/06/2024'
    },
    {
        title: 'Thành Công Với Kinh Doanh Trực Tuyến: Hành Trình Từ A Đến Z',
        des: 'Kinh doanh trực tuyến không chỉ là một xu hướng mà còn là cơ hội để bạn kiếm định bản thân và tạo ra nguồn thu nhập ổn định.',
        img: Teamwork,
        date: '24/06/2024'
    },
]

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

const outstanding = getRandomItem(articles)
const articleFeatures = getRemainingItems(articles, outstanding)

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
</script>

<template>
    <div class="w-full px-6 md:px-[10%] lg:px-[20%] py-[60px] md:py-[80px]">
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

            <!-- <div class="flex justify-end mb-6">
                
            </div> -->

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                <!-- Featured Article -->
                <div class="featured-article bg-white rounded-lg overflow-hidden transform transition-transform duration-300 hover:-translate-y-1"
                    @mouseover="hoveredArticle = 'dropship'" @mouseleave="hoveredArticle = null">
                    <div class="relative h-56 md:h-64">
                        <img :src="outstanding.img" alt="Featured Article"
                            class="w-full h-full rounded-16px object-cover">
                        <div class="absolute inset-0 bg-gradient-to-t rounded-16px from-black/50 to-transparent"></div>
                    </div>
                    <div>
                        <h2 class="text-16px font-bold py-3 cursor-pointer">{{ outstanding.title }}
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
                            <div class="md:w-1/3 h-40 overflow-hidden">
                                <img :src="item.img" alt="Article image"
                                    class="w-full h-full object-cover rounded-12px">
                            </div>
                            <div class="flex-1">
                                <div class="flex flex-col justify-between items-start mb-1">
                                    <h3 class="text-16px font-bold cursor-pointer">{{ item.title }}</h3>
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