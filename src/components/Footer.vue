<script setup lang="ts">
// import Facebook from "@/public/social_facebook.png"
// import Instagram from "@/public/social_instagram.png"

const footerLinks = {
    'Trang': [
        { label: 'Trang chủ', path: '/' },
        { label: 'Bộ sưu tập', path: '/collections' },
        { label: 'Dịch vụ', path: '/service' },
        { label: 'Về chúng tôi', path: '/about' }
    ],
    'Bộ sưu tập': [
        { label: 'Bộ sưu tập 1', path: '/bst1' },
        { label: 'Bộ sưu tập 2', path: '/bst2' },
        { label: 'Bộ sưu tập 3', path: '/bst3' },
        { label: 'Bộ sưu tập 4', path: '/bst4' }
    ],
    'Liên hệ': [
        { label: 'Vinhome Smartcity', path: 'mailto:info@bdesign.com' },
        { label: 'bdesign@gmail.com', path: 'bdesign@gmail.com' },
        { label: '0961717906', path: '0961717906' }
    ]
};

const socialLinks = [
    { icon: 'facebook', path: '1', redirect: 'https://www.facebook.com/talafanMU' },
    { icon: 'instagram', path: '2', redirect: 'https://www.instagram.com/thuongg149/' },
    // { icon: 'twitter', path: 'https://twitter.com', }
];
</script>

<template>
    <footer class="mt-24 pt-16 pb-8 border-t-1 border-#C9C9C9 ">
        <div class="container mx-auto px-4">
            <!-- Main Footer Content -->
            <div class="flex flex-col gap-8 mb-12 justify-center md:(justify-start flex-row)">
                <!-- Brand Section -->
                <div class="grow-2 text-center max-w-393px md:text-left">
                    <NuxtLink to="/" class="text-40px font-bold flex gap-2 md:justify-start justify-center items-end playfair-display text-#292F36">
                        <img src="@/public/logo.png" class="pb-3 h-48px" />
                        Design
                    </NuxtLink>

                    <p class="text-gray-600 mb-6 text-22px md:px-0 px-2">
                        Thiết kế theo yêu cầu, định hình phong cách của bạn
                    </p>
                    <div class="flex gap-54px space-x-4 md:justify-start justify-center">
                        <a v-for="social in socialLinks" :key="social.icon" :href="social.redirect" target="_blank"
                            rel="noopener noreferrer" class="text-gray-600 hover:text-black transition-colors">
                            <img :src="social.path" alt="social">
                            <!-- <span class="sr-only">{{ social.icon }}</span> -->
                            <!-- <i :class="'fab fa-' + social.icon"></i> -->
                        </a>
                    </div>
                </div>

                <!-- Footer Links -->
                <template v-for="(links, title) in footerLinks" :key="title">
                    <div class="grow-1 md:(block text-left) flex flex-col items-center text-center" :class="{'grow-2' :title === 'Liên hệ'}">
                        <h4 class="font-500 mb-4 text-25px playfair-display">{{ title }}</h4>
                        <ul class="space-y-2">
                            <li v-for="link in links" :key="link.path">
                                <NuxtLink :to="link.path"
                                    class="text-#4D5053 text-22px font-400 hover:text-black transition-colors">
                                    {{ link.label }}
                                </NuxtLink>
                            </li>
                        </ul>
                    </div>
                </template>

            </div>

            <!-- Copyright -->
            <div class="border-t border-gray-200 pt-8">
                <p class="text-center text-gray-600 text-sm">
                    © {{ new Date().getFullYear() }} B Design. All rights reserved.
                </p>
            </div>
        </div>
    </footer>
</template>

<style scoped>
.container {
    max-width: 1152px;
}

/* Smooth transitions */
.transition-colors {
    transition-property: color;
    transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
    transition-duration: 300ms;
}

.playfair-display {
    font-family: "Playfair Display", serif;
    font-optical-sizing: auto;
    font-weight: 500;
    font-style: normal;
}
</style>