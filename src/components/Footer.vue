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
    <footer class="px-6 md:px-[10%] lg:px-[20%] py-[60px] md:py-[80px] bg-[#fbc04d] text-black ">
        <div class="container mx-auto px-4">
            <div class="flex flex-col md:flex-row justify-between gap-8">
                <!-- Logo + Info -->
                <div class="space-y-3 max-w-sm">
                    <img src="../public/logo_black.png" alt="Innovator Academy" />
                    <div class="flex items-center gap-2">
                        <img src="../public/gmail.png" class="h-18px" alt="gmail-logo">
                        <span>Innovatoracademy@gmail.com</span>
                    </div>
                    <div class="flex items-center gap-2">
                        <img src="../public/Call.png" class="h-18px" alt="call-logo">
                        <span>+8435 731 9979</span>
                    </div>
                    <div class="flex items-center gap-2">
                        <img src="../public/location.png" class="h-18px" alt="location-logo">
                        <span>
                            Tầng 7, toà nhà Milk Group, 212 - 214 Nguyễn Trãi, Thanh Xuân, Hà Nội
                        </span>
                    </div>
                </div>

                <!-- Giới thiệu -->
                <div>
                    <h3 class="font-semibold mb-3">Giới thiệu</h3>
                    <ul class="space-y-1">
                        <li><a href="#" class="hover:underline">Sản phẩm và dịch vụ</a></li>
                        <li><a href="#" class="hover:underline">Phương pháp đào tạo</a></li>
                        <li><a href="#" class="hover:underline">Đội ngũ giảng viên</a></li>
                        <li><a href="#" class="hover:underline">Thành tựu và dự án</a></li>
                    </ul>
                </div>

                <!-- Về chúng tôi -->
                <div>
                    <h3 class="font-semibold mb-3">Về chúng tôi</h3>
                    <ul class="space-y-1">
                        <li><a href="#" class="hover:underline">Sứ mệnh và tầm nhìn</a></li>
                        <li><a href="#" class="hover:underline">Giá trị cốt lõi</a></li>
                        <li><a href="#" class="hover:underline">Đối tác và hợp tác</a></li>
                        <li><a href="#" class="hover:underline">Chính sách và điều khoản</a></li>
                    </ul>
                </div>

                <!-- Kết nối -->
                <div>
                    <h3 class="font-semibold mb-3">Kết nối với chúng tôi</h3>
                    <div class="flex gap-4">
                        <a href="#"><i class='bx bxl-facebook-circle text-20px'></i></a>
                        <a href="#"><i class='bx bxl-twitter text-20px'></i></a>
                        <a href="#"><i class='bx bxl-linkedin-square text-20px'></i></a>
                    </div>
                </div>
            </div>

            <!-- Bottom line -->
            <div class="border-t border-black mt-8 pt-4 text-center text-sm">
                © 2024 Design by GabDol
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