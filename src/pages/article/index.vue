<script lang="ts" setup>

// Pagination state
const currentPage = ref(1);
const itemsPerPage = ref(9);
const maxVisibleButtons = 5;
const selectedDate = ref('all');
const filteredArticles = ref([...articles.value]);

// Sort articles by date (newest first)
onMounted(() => {
    sortArticlesByDate();
});

const sortArticlesByDate = () => {
    filteredArticles.value.sort((a, b) => {
        const dateA = convertToDate(a.date);
        const dateB = convertToDate(b.date);
        return dateB.getTime() - dateA.getTime();
    });
};

const convertToDate = (dateString: string) => {
    const [day, month, year] = dateString.split('/');
    return new Date(parseInt(year), parseInt(month) - 1, parseInt(day));
};

const filterByDate = () => {
    currentPage.value = 1;

    if (selectedDate.value === 'all') {
        filteredArticles.value = [...articles.value];
    } else {
        const today = new Date();
        const filteredResults = articles.value.filter(article => {
            const articleDate = convertToDate(article.date);

            if (selectedDate.value === 'today') {
                return articleDate.getDate() === today.getDate() &&
                    articleDate.getMonth() === today.getMonth() &&
                    articleDate.getFullYear() === today.getFullYear();
            } else if (selectedDate.value === 'week') {
                const weekAgo = new Date(today);
                weekAgo.setDate(today.getDate() - 7);
                return articleDate >= weekAgo && articleDate <= today;
            } else if (selectedDate.value === 'month') {
                return articleDate.getMonth() === today.getMonth() &&
                    articleDate.getFullYear() === today.getFullYear();
            }

            return true;
        });

        filteredArticles.value = filteredResults;
    }

    sortArticlesByDate();
};

const totalPages = computed(() => {
    return Math.ceil(filteredArticles.value.length / itemsPerPage.value);
});

const displayedArticles = computed(() => {
    const startIndex = (currentPage.value - 1) * itemsPerPage.value;
    const endIndex = startIndex + itemsPerPage.value;
    return filteredArticles.value.slice(startIndex, endIndex);
});

const visiblePageNumbers = computed(() => {
    const halfWay = Math.ceil(maxVisibleButtons / 2);

    if (totalPages.value <= maxVisibleButtons) {
        return Array.from({ length: totalPages.value }, (_, i) => i + 1);
    }

    if (currentPage.value <= halfWay) {
        return Array.from({ length: maxVisibleButtons }, (_, i) => i + 1);
    }

    if (currentPage.value > totalPages.value - halfWay) {
        return Array.from(
            { length: maxVisibleButtons },
            (_, i) => totalPages.value - maxVisibleButtons + i + 1
        );
    }

    return Array.from(
        { length: maxVisibleButtons },
        (_, i) => currentPage.value - halfWay + i + 1
    );
});

const goToPage = (page: number) => {
    currentPage.value = page;
    scrollToTop();
};

const goToPrevPage = () => {
    if (currentPage.value > 1) {
        currentPage.value--;
        scrollToTop();
    }
};

const goToNextPage = () => {
    if (currentPage.value < totalPages.value) {
        currentPage.value++;
        scrollToTop();
    }
};

const updateItemsPerPage = () => {
    currentPage.value = 1;
};

const scrollToTop = () => {
    window.scrollTo({
        top: 0,
        behavior: 'smooth'
    });
};

const formatDate = (dateString: string) => {
    return dateString;
};

const router = useRouter()
function goToDetailArticle(id: string) {
    router.push(`/article/${id}`)
}
</script>

<template>
    <div class="max-w-6xl mx-auto mt-64px px-4 py-8 md:py-12">
        <div class="flex flex-col md:flex-row justify-between items-center mb-8">
            <h1 class="text-2xl font-bold">Bài viết</h1>
            <div class="date-filter mt-4 md:mt-0">
                <select v-model="selectedDate"
                    class="border rounded px-3 py-2 focus:outline-none focus:ring-2 focus:ring-blue-300 transition-all"
                    @change="filterByDate">
                    <option value="all">Tất cả</option>
                    <option value="today">Hôm nay</option>
                    <option value="week">Tuần này</option>
                    <option value="month">Tháng này</option>
                </select>
            </div>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
            <div v-for="(article, index) in displayedArticles" :key="index"
                class="bg-white rounded-lg overflow-hidden shadow-md hover:shadow-lg transition-shadow duration-300">
                <div class="relative overflow-hidden p-4">
                    <img :src="article.image" :alt="article.title"
                        class="w-full h-48 rounded-lg object-cover transform hover:scale-105 transition-transform duration-300">
                    <div class="mt-16px w-fit bg-#DDF9FF text-#37C4E5 text-xs px-4 py-2 rounded-lg">{{
                        article.category }}</div>
                </div>
                <div class="p-4">
                    <h2 @click="goToDetailArticle(article.id)" class="font-bold text-lg mb-2 cursor-pointer">{{
                        article.title }}</h2>
                    <p class="text-gray-500 text-sm">{{ formatDate(article.date) }}</p>
                </div>
            </div>
        </div>

        <div class="pagination flex justify-center items-center mt-8">
            <button @click="goToPrevPage" :disabled="currentPage === 1" class="mx-1 px-3 py-1 rounded border"
                :class="currentPage === 1 ? 'text-gray-400 cursor-not-allowed' : 'hover:bg-gray-100'">
                &lt;
            </button>

            <button v-for="page in visiblePageNumbers" :key="page" @click="goToPage(page)"
                class="mx-1 px-3 py-1 rounded border"
                :class="currentPage === page ? 'bg-blue-500 text-white' : 'hover:bg-gray-100'">
                {{ page }}
            </button>

            <span v-if="totalPages > maxVisibleButtons && currentPage < totalPages - maxVisibleButtons / 2"
                class="mx-1">...</span>

            <button v-if="totalPages > maxVisibleButtons" @click="goToPage(totalPages)"
                class="mx-1 px-3 py-1 rounded border"
                :class="currentPage === totalPages ? 'bg-blue-500 text-white' : 'hover:bg-gray-100'">
                {{ totalPages }}
            </button>

            <button @click="goToNextPage" :disabled="currentPage === totalPages" class="mx-1 px-3 py-1 rounded border"
                :class="currentPage === totalPages ? 'text-gray-400 cursor-not-allowed' : 'hover:bg-gray-100'">
                &gt;
            </button>

            <!-- <div class="flex items-center ml-4">
                <select v-model="itemsPerPage" class="border rounded px-2 py-1 text-sm" @change="updateItemsPerPage">
                    <option value="9">9</option>
                    <option value="10">10</option>
                    <option value="20">20</option>
                    <option value="30">30</option>
                    <option value="40">40</option>
                </select>
            </div> -->
        </div>
    </div>
</template>
  
  
  
<style scoped>
.pagination button {
    transition: all 0.2s ease;
}

.pagination button:hover:not(:disabled) {
    transform: translateY(-1px);
}

.pagination button:active:not(:disabled) {
    transform: translateY(0);
}

img {
    transition: transform 0.3s ease;
}

.date-filter select {
    appearance: none;
    background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='currentColor' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3e%3cpolyline points='6 9 12 15 18 9'%3e%3c/polyline%3e%3c/svg%3e");
    background-repeat: no-repeat;
    background-position: right 0.5rem center;
    background-size: 1em;
    padding-right: 2rem;
}
</style>