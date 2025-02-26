<template>
    <div class="flex flex-col items-center justify-center min-h-screen bg-gray-100 p-6">
        <div class="w-full max-w-md bg-white p-6 rounded-lg shadow-md">
            <input type="text" v-model="passwordInput" placeholder="輸入密碼"
                class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" />

            <p class="mt-4 text-lg font-semibold">密碼強度：</p>
            <h3 v-if="passwordStrength === null" class="text-gray-500 text-lg font-bold">
                請輸入密碼
            </h3>
            <h3 v-else-if="passwordStrength === 0" class="text-red-500 text-lg font-bold">
                你的密碼過於簡單，容易被破解。
            </h3>
            <h3 v-else-if="passwordStrength === 1" class="text-yellow-500 text-lg font-bold">
                密碼稍微有變化，但仍然較弱。
            </h3>
            <h3 v-else-if="passwordStrength === 2" class="text-green-500 text-lg font-bold">
                你的密碼已經包含多種類型的字符，但仍有提升空間。
            </h3>
            <h3 v-else-if="passwordStrength === 3" class="text-blue-500 text-lg font-bold">
                你的密碼相對安全，包含大小寫字母、數字與特殊符號，且長度超過 10 位。
            </h3>
            <h3 v-else class="text-purple-500 text-lg font-bold">
                你的密碼非常安全，幾乎不可能被暴力破解。
            </h3>
        </div>
    </div>
</template>

<script setup>
import { ref, watchEffect } from 'vue';
import zxcvbn from 'zxcvbn';

const passwordInput = ref('');
const passwordStrength = ref(null);

watchEffect(() => {
    if (passwordInput.value !== '') {
        passwordStrength.value = zxcvbn(passwordInput.value).score
    } else {
        passwordStrength.value = null
    }
})
</script>