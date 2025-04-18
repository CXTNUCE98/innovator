<script setup lang="ts">
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
                <h1 class="text-3xl font-bold text-gray-800">Bài viết nổi bật</h1>
                <p class="text-gray-600 mt-1">Tổng hợp các bài viết chia sẻ về kinh nghiệm miễn phí và các tin tức sự kiện
                </p>
            </header>

            <div class="flex justify-end mb-6">
                <button
                    class="bg-gray-100 hover:bg-gray-200 text-gray-800 px-4 py-2 rounded-md transition-colors duration-300">
                    Xem tất cả
                </button>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                <!-- Featured Article -->
                <div class="featured-article bg-white rounded-lg overflow-hidden transform transition-transform duration-300 hover:-translate-y-1"
                    @mouseover="hoveredArticle = 'dropship'" @mouseleave="hoveredArticle = null">
                    <div class="relative">
                        <img src="../public/dropship_article.png" alt="Dropshipping" class="w-full object-cover">
                        <div class="absolute inset-0 bg-gradient-to-t from-black/50 to-transparent"></div>
                    </div>
                    <div class="pt-20px">
                        <span
                            class="inline-block bg-blue-100 text-blue-500 px-3 py-1 text-xs rounded-full font-medium mb-3">Dropship</span>
                        <h2 class="text-16px font-bold mb-3">Bí Quyết Thành Công Với Dropship: Khám Phá Chiến Lược Đỉnh Cao
                        </h2>
                        <p class="text-gray-600 text-14px mb-4">Bạn đang muốn khởi nghiệp với mô hình dropship nhưng chưa
                            biết bắt đầu
                            từ đâu? Hãy cùng chúng tôi khám phá những chiến lược đỉnh cao để xây dựng một cửa hàng dropship
                            thành công. Khóa học của chúng tôi sẽ trang bị cho bạn kiến thức từ cơ bản đến nâng cao, giúp
                            bạn tự tin trên con đường kinh doanh trực tuyến.</p>
                        <div class="text-gray-500 text-sm">24/06/2024</div>
                    </div>
                </div>

                <!-- Right Column Articles -->
                <div class="space-y-8">
                    <!-- Amazon Article -->
                    <div class="article-card flex flex-col md:flex-row gap-20px bg-white rounded-lg overflow-hidden transform transition-transform duration-300 hover:-translate-y-1"
                        @mouseover="hoveredArticle = 'amazon'" @mouseleave="hoveredArticle = null">
                        <img src="../public/amazon_article.png" alt="Amazon"
                            class="h-140px rounded object-center object-cover">
                        <div class="flex-1">
                            <div class="flex flex-col justify-between items-start mb-1">
                                <h3 class="text-16px font-bold">Làm Chủ Sàn Amazon: Từ Người Mới Đến Chuyên Gia</h3>
                                <span
                                    class="inline-block bg-blue-100 text-blue-500 px-2 py-1 text-xs rounded-full font-medium">Dropship</span>
                            </div>
                            <p class="text-gray-600 text-12px mb-3">Amazon là một thị trường tiềm năng nhưng cũng đầy thách
                                thức. Để trở thành người bán hàng thành công trên Amazon sử dụng công cụ quảng cáo hiệu quả.
                            </p>
                            <div class="text-gray-500 text-xs">24/06/2024</div>
                        </div>
                    </div>

                    <!-- Livestream Article -->
                    <div class="article-card flex flex-col md:flex-row gap-20px bg-white rounded-lg overflow-hidden transform transition-transform duration-300 hover:-translate-y-1"
                        @mouseover="hoveredArticle = 'livestream'" @mouseleave="hoveredArticle = null">
                        <img src="../public/livestream_article.png" alt="Livestream" class="h-140px rounded object-cover">
                        <div class="flex-1">
                            <div class="flex justify-between flex-col items-start mb-2">
                                <h3 class="text-lg font-bold">Livestream Bán Hàng: Nghệ Thuật Tăng Doanh Số Tức Thì</h3>
                                <span
                                    class="inline-block bg-blue-100 text-blue-500 px-2 py-1 text-xs rounded-full font-medium">Dropship</span>
                            </div>
                            <p class="text-gray-600 text-12px mb-3">Livestream bán hàng đang trở thành xu hướng hot giúp
                                tăng
                                doanh số một cách nhanh chóng. Những ảnh hưởng nào để thực hiện một buổi livestream thành
                                công?</p>
                            <div class="text-gray-500 text-xs">24/06/2024</div>
                        </div>
                    </div>

                    <!-- Online Business Article -->
                    <div class="article-card flex flex-col md:flex-row gap-20px bg-white rounded-lg overflow-hidden transform transition-transform duration-300 hover:-translate-y-1"
                        @mouseover="hoveredArticle = 'online'" @mouseleave="hoveredArticle = null">
                        <img src="../public/teamwork_article.png" alt="Online Business"
                            class="h-140px rounded object-cover">
                        <div class="flex-1">
                            <div class="flex justify-between flex-col items-start mb-2">
                                <h3 class="text-16px font-bold">Thành Công Với Kinh Doanh Trực Tuyến: Hành Trình Từ A Đến Z
                                </h3>
                                <span
                                    class="inline-block bg-blue-100 text-blue-500 px-2 py-1 text-xs rounded-full font-medium">Dropship</span>
                            </div>
                            <p class="text-gray-600 text-sm mb-3">Kinh doanh trực tuyến không chỉ là một xu hướng mà còn là
                                cơ hội để bạn kiếm định bản thân và tạo ra nguồn thu nhập ổn định.</p>
                            <div class="text-gray-500 text-xs">24/06/2024</div>

                        </div>
                    </div>
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