<script setup lang="ts">
import { ref, reactive } from 'vue'
import Location from '@/public/location.png'
import Call from '@/public/Call.png'
import Email from '@/public/gmail.png'

// Form state
const formData = reactive({
    phone: '',
    email: '',
    message: ''
})

const isLoading = ref(false)
const formSubmitted = ref(false)

// Form validation
const formErrors = reactive({
    phone: '',
    email: '',
    message: ''
})

const validateForm = () => {
    let isValid = true

    // Reset errors
    Object.keys(formErrors).forEach(key => {
        formErrors[key as keyof typeof formErrors] = ''
    })

    // Validate phone
    if (!formData.phone.trim()) {
        formErrors.phone = 'Vui lòng nhập số điện thoại'
        isValid = false
    }

    // Validate email
    if (!formData.email.trim()) {
        formErrors.email = 'Vui lòng nhập email'
        isValid = false
    } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(formData.email)) {
        formErrors.email = 'Email không hợp lệ'
        isValid = false
    }

    // Validate message
    if (!formData.message.trim()) {
        formErrors.message = 'Vui lòng nhập nội dung'
        isValid = false
    }

    return isValid
}

const handleSubmit = async () => {
    if (!validateForm()) return

    isLoading.value = true

    try {
        // Simulate API call
        await new Promise(resolve => setTimeout(resolve, 1000))

        // Reset form
        Object.keys(formData).forEach(key => {
            formData[key as keyof typeof formData] = ''
        })

        formSubmitted.value = true

        // Reset success message after 3 seconds
        setTimeout(() => {
            formSubmitted.value = false
        }, 3000)

    } catch (error) {
        console.error('Error submitting form:', error)
    } finally {
        isLoading.value = false
    }
}

// Contact information
const contactInfo = [
    {
        icon: 'bx bx-location-plus',
        label: 'Địa chỉ',
        value: 'Tầng 7, tòa nhà Milk Group, 212 - 214 Nguyễn Trãi, Thanh Xuân, Hà Nội'
    },
    {
        icon: 'bx bxs-phone',
        label: 'Số điện thoại',
        value: '+84 35 731 9978'
    },
    {
        icon: 'bx bxs-envelope',
        label: 'Email',
        value: 'Innovatoracademy@gmail.com'
    }
]


</script>

<template>
    <SharedHeaderPage title="Hãy liên lạc để có một điều gì đó tuyệt vời cùng nhau..."
        subTitle="Innovator Academy quyết tâm trở thành một trung tâm đào tạo hàng đầu, là nguồn lực đáng tin cậy cho sự phát triển nhân lực ưu tú, có khả năng thích ứng linh hoạt với công nghệ 4.0 và đóng góp tích cực vào sự phát triển bền vững của cộng đồng và xã hội." />
    <div class="min-h-screen bg-gray-50 py-8">
        <div class="max-w-6xl mx-auto px-2">
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                <!-- Info -->
                <div class="space-y-4">
                    <div v-for="info in contactInfo" :key="info.label" class="flex items-center bg-white rounded-xl shadow p-4">
                        <div class="flex items-center justify-center w-8 h-8 bg-#FFFBF1 rounded-full mr-4">
                            <!-- <img :src="info.icon" class="h-18px bg-#fcaf17" alt="location-logo"> -->
                            <i :class='info.icon' class="text-#fcaf17"></i>
                        </div>
                        <div>
                            <div class="font-semibold text-gray-800">{{ info.label }}</div>
                            <div class="text-gray-600 text-sm">{{ info.value }}</div>
                        </div>
                    </div>
                </div>
                <!-- Form -->
                <div class="bg-white rounded-xl shadow p-6">
                    <div class="font-bold text-lg mb-2">Gửi tin nhắn cho chúng tôi</div>
                    <div class="text-gray-500 text-sm mb-4">Thông tin cá nhân của bạn sẽ được chúng tôi bảo mật tuyệt đối</div>
                    <form @submit.prevent="handleSubmit" class="space-y-4">
                        <div>
                            <input v-model="formData.phone" type="text" placeholder="Số điện thoại"
                                class="w-full px-4 py-2 border rounded focus:ring-2 focus:ring-yellow-400"
                                :class="{ 'border-red-500': formErrors.phone }" />
                            <div v-if="formErrors.phone" class="text-red-500 text-xs mt-1">{{ formErrors.phone }}</div>
                        </div>
                        <div>
                            <input v-model="formData.email" type="email" placeholder="Địa chỉ email"
                                class="w-full px-4 py-2 border rounded focus:ring-2 focus:ring-yellow-400"
                                :class="{ 'border-red-500': formErrors.email }" />
                            <div v-if="formErrors.email" class="text-red-500 text-xs mt-1">{{ formErrors.email }}</div>
                        </div>
                        <div>
                            <textarea v-model="formData.message" rows="4" placeholder="Bạn muốn nhắn nhủ điều gì với chúng tôi không ^^"
                                class="w-full px-4 py-2 border rounded focus:ring-2 focus:ring-yellow-400 resize-none"
                                :class="{ 'border-red-500': formErrors.message }" />
                            <div v-if="formErrors.message" class="text-red-500 text-xs mt-1">{{ formErrors.message }}</div>
                        </div>
                        <button type="submit" :disabled="isLoading"
                            class="bg-yellow-400 hover:bg-yellow-500 text-white font-semibold py-2 px-6 rounded transition w-full">
                            {{ isLoading ? 'Đang gửi...' : 'Gửi thông tin' }}
                        </button>
                        <div v-if="formSubmitted" class="text-green-600 text-sm mt-2">Gửi thành công!</div>
                    </form>
                </div>
            </div>
            <!-- Map -->
            <div class="mt-8">
                <iframe
                    class="w-full rounded-2xl h-72 md:h-96 border-0"
                    src="https://www.google.com/maps?q=21.002085,105.815821&z=17&output=embed"
                    allowfullscreen
                    loading="lazy"
                ></iframe>
            </div>
        </div>
    </div>
</template>

<style scoped>
/* Custom focus styles */
input:focus,
textarea:focus {
    outline: none;
}

/* Smooth transitions */
.transition-colors {
    transition: color 0.2s ease-in-out, background-color 0.2s ease-in-out, border-color 0.2s ease-in-out;
}

/* Loading animation */
@keyframes spin {
    from {
        transform: rotate(0deg);
    }

    to {
        transform: rotate(360deg);
    }
}

.bx-spin {
    animation: spin 1s linear infinite;
}
</style>