<script setup lang="ts">
import { ref, reactive, watch } from 'vue'

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

// Real-time validation
const validateField = (field: keyof typeof formData, value: string) => {
    switch (field) {
        case 'phone':
            if (!value.trim()) {
                formErrors.phone = 'Vui lòng nhập số điện thoại'
            } else {
                formErrors.phone = ''
            }
            break
        case 'email':
            if (!value.trim()) {
                formErrors.email = 'Vui lòng nhập email'
            } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(value)) {
                formErrors.email = 'Email không hợp lệ'
            } else {
                formErrors.email = ''
            }
            break
        case 'message':
            if (!value.trim()) {
                formErrors.message = 'Vui lòng nhập nội dung'
            } else {
                formErrors.message = ''
            }
            break
    }
}

// Watch for changes and validate in real-time
watch(() => formData.phone, (newValue) => {
    validateField('phone', newValue)
})

watch(() => formData.email, (newValue) => {
    validateField('email', newValue)
})

watch(() => formData.message, (newValue) => {
    validateField('message', newValue)
})

const validateForm = () => {
    let isValid = true

    // Validate all fields
    validateField('phone', formData.phone)
    validateField('email', formData.email)
    validateField('message', formData.message)

    // Check if any errors exist
    if (formErrors.phone || formErrors.email || formErrors.message) {
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
        icon: 'bx bxs-location-plus',
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
    <div class="min-h-screen bg-gray-50 pt-16 pb-12">
        <div class="max-w-6xl mx-auto px-2">
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                <!-- Info -->
                <div class="flex flex-col justify-between gap-2">
                    <div v-for="info in contactInfo" :key="info.label"
                        class="flex items-center bg-white rounded-xl shadow p-8">
                        <div class="flex items-center justify-center w-12 h-12 bg-#FFFBF1 rounded-full mr-4">
                            <i :class='info.icon' class="text-#fcaf17 text-20px"></i>
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
                    <div class="text-gray-500 text-sm mb-4">Thông tin cá nhân của bạn sẽ được chúng tôi bảo mật tuyệt
                        đối</div>
                    <form @submit.prevent="handleSubmit" class="space-y-4">
                        <div class="flex flex-col md:flex-row gap-4">
                            <div class="flex-1">
                                <div class="relative">
                                    <input v-model="formData.phone"
                                        class="peer w-full bg-transparent placeholder:text-slate-400 text-slate-700 text-sm border border-slate-200 rounded-md px-3 py-3 transition duration-300 ease focus:outline-none focus:border-slate-400 hover:border-slate-300 shadow-sm focus:shadow"
                                        :class="{ '!border-red-500': formErrors.phone }" />
                                    <div v-if="formErrors.phone" class="text-red-500 text-xs mt-1">{{ formErrors.phone
                                    }}
                                    </div>
                                    <label
                                        class="absolute cursor-text bg-white px-1 left-2.5 text-slate-400 text-sm transition-all transform origin-left pointer-events-none z-10"
                                        :class="[
                                            formData.phone.trim() || 'peer-focus:-top-2 peer-focus:left-2.5 peer-focus:text-xs peer-focus:text-slate-400 peer-focus:scale-90',
                                            formData.phone.trim() ? '-top-2 left-2.5 text-xs text-slate-400 scale-90' : 'top-3'
                                        ]">
                                        Số điện thoại <span class="text-red-500">*</span>
                                    </label>
                                </div>
                            </div>
                            <div class="flex-1">
                                <div class="relative">
                                    <input v-model="formData.email"
                                        class="peer w-full bg-transparent placeholder:text-slate-400 text-slate-700 text-sm border border-slate-200 rounded-md px-3 py-3 transition duration-300 ease focus:outline-none focus:border-slate-400 hover:border-slate-300 shadow-sm focus:shadow"
                                        :class="{ '!border-red-500': formErrors.email }" />
                                    <div v-if="formErrors.email" class="text-red-500 text-xs mt-1">{{ formErrors.email
                                    }}
                                    </div>
                                    <label
                                        class="absolute cursor-text bg-white px-1 left-2.5 text-slate-400 text-sm transition-all transform origin-left pointer-events-none z-10"
                                        :class="[
                                            formData.email.trim() || 'peer-focus:-top-2 peer-focus:left-2.5 peer-focus:text-xs peer-focus:text-slate-400 peer-focus:scale-90',
                                            formData.email.trim() ? '-top-2 left-2.5 text-xs text-slate-400 scale-90' : 'top-3'
                                        ]">
                                        Địa chỉ email <span class="text-red-500">*</span>
                                    </label>
                                </div>
                            </div>
                        </div>

                        <div>
                            <textarea v-model="formData.message" rows="6"
                                placeholder="Bạn muốn nhắn nhủ điều gì với chúng tôi không ^^"
                                class="w-full px-4 py-3 border border-slate-200 rounded-md focus:border-slate-400 hover:border-slate-300 resize-none text-slate-700 text-sm transition duration-300 ease focus:outline-none shadow-sm focus:shadow"
                                :class="{ '!border-red-500': formErrors.message }" />
                            <div v-if="formErrors.message" class="text-red-500 text-xs mt-1">{{ formErrors.message }}
                            </div>
                        </div>
                        <button type="submit" :disabled="isLoading"
                            class="bg-yellow-400 hover:bg-yellow-500 text-white font-semibold py-3 px-6 rounded-md transition  disabled:opacity-50 disabled:cursor-not-allowed">
                            {{ isLoading ? 'Đang gửi...' : 'Gửi thông tin' }}
                        </button>
                        <div v-if="formSubmitted" class="text-green-600 text-sm mt-2 text-center">Gửi thành công!</div>
                    </form>
                </div>
            </div>
            <!-- Map -->
            <div class="mt-8">
                <iframe class="w-full rounded-2xl h-72 md:h-96 border-0"
                    src="https://www.google.com/maps?q=21.002085,105.815821&z=17&output=embed" allowfullscreen
                    loading="lazy"></iframe>
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