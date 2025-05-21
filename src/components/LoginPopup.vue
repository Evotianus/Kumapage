<template>
    <div v-if="isOpen" class="fixed inset-0 flex items-center justify-center z-40"
        style="background-color: rgba(0, 0, 0, 0.5)">
        <div class="bg-white rounded-lg shadow-xl w-full max-w-md mx-4 z-50">
            <!-- Header -->
            <div class="flex justify-between items-center px-6 py-4 bg-gray-400 rounded-t-lg">
                <h2 class="text-xl font-semibold">Sign In</h2>
                <button @click="handleClose" class="text-gray-700 hover:text-gray-900">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                        stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                        <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                        <path d="M18 6l-12 12" />
                        <path d="M6 6l12 12" />
                    </svg>
                </button>
            </div>

            <!-- Login Fields -->
            <div class="p-6">
                <div class="mb-4">
                    <label for="email" class="block text-sm font-medium text-gray-700 mb-1">
                        Email
                    </label>
                    <div class="relative">
                        <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24"
                                fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                stroke-linejoin="round" class="text-gray-500">
                                <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                                <path
                                    d="M3 7a2 2 0 0 1 2 -2h14a2 2 0 0 1 2 2v10a2 2 0 0 1 -2 2h-14a2 2 0 0 1 -2 -2v-10z" />
                                <path d="M3 7l9 6l9 -6" />
                            </svg>
                        </div>
                        <input id="email" type="email"
                            class="bg-gray-100 block w-full pl-10 pr-3 py-2 border border-gray-300 rounded-full text-gray-900 focus:outline-none focus:ring-2 focus:ring-gray-500"
                            placeholder="you@example.com" v-model="email" />
                    </div>
                </div>

                <div class="mb-8">
                    <label for="password" class="block text-sm font-medium text-gray-700 mb-1">
                        Password
                    </label>
                    <div class="relative">
                        <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24"
                                fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                stroke-linejoin="round" class="text-gray-500">
                                <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                                <path
                                    d="M5 11m0 2a2 2 0 0 1 2 -2h10a2 2 0 0 1 2 2v6a2 2 0 0 1 -2 2h-10a2 2 0 0 1 -2 -2z" />
                                <path d="M17 11v-4a5 5 0 0 0 -10 0v4" />
                            </svg>
                        </div>
                        <input id="password" type="password"
                            class="bg-gray-100 block w-full pl-10 pr-3 py-2 border border-gray-300 rounded-full text-gray-900 focus:outline-none focus:ring-2 focus:ring-gray-500"
                            placeholder="••••••••" v-model="password" />
                    </div>
                </div>

                <!-- Error message display -->
                <div v-if="errorMessage" class="mb-4 text-red-500 text-sm">
                    {{ errorMessage }}
                </div>

                <div>
                    <button @click="handleLogin"
                        class="w-full flex justify-center items-center gap-2 bg-gray-200 px-4 py-2 rounded-full font-semibold hover:bg-gray-300 transition duration-200"
                        :disabled="isLoading">
                        <svg v-if="!isLoading" xmlns="http://www.w3.org/2000/svg" width="20" height="20"
                            viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"
                            stroke-linecap="round" stroke-linejoin="round">
                            <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                            <path d="M14 8v-2a2 2 0 0 0 -2 -2h-7a2 2 0 0 0 -2 2v12a2 2 0 0 0 2 2h7a2 2 0 0 0 2 -2v-2" />
                            <path d="M20 12h-13l3 -3" />
                            <path d="M7 15l-3 -3" />
                        </svg>
                        <svg v-if="isLoading" class="animate-spin h-5 w-5 text-gray-700"
                            xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                            <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4">
                            </circle>
                            <path class="opacity-75" fill="currentColor"
                                d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z">
                            </path>
                        </svg>
                        {{ isLoading ? 'Signing In...' : 'Sign In' }}
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, watch } from 'vue';
import axios from 'axios';

axios.defaults.baseURL = import.meta.env.VITE_API_BASE_URL + "/api"
axios.defaults.headers.common["Authorization"] = "Bearer 66tR3dHK19eZMR8qfvtvgFH7KBdmDsot2sk3iuyzyyTDRcvh6uY6iAOqk5MvQdtc"

const props = defineProps({
    show: {
        type: Boolean,
        default: false
    }
});

// Define emits including login-success event
const emit = defineEmits(['close', 'login-success']);

const isOpen = ref(props.show);
const email = ref('');
const password = ref('');
const isLoading = ref(false);
const errorMessage = ref('');

watch(() => props.show, (newVal) => {
    isOpen.value = newVal;
    if (newVal) {
        // Clear form when opening
        email.value = '';
        password.value = '';
        errorMessage.value = '';
    }
});

function handleClose() {
    isOpen.value = false;
    emit('close');
}

async function handleLogin() {
    if (!email.value || !password.value) {
        errorMessage.value = 'Email and password are required';
        return;
    }

    errorMessage.value = '';
    isLoading.value = true;

    try {
        const response = await axios.post('/auth/login', {
            email: email.value,
            password: password.value
        });

        console.log('Login successful:', response.data);

        // Extract user data and token from response
        const userData = response.data.user || { email: email.value };
        const token = response.data.token || response.data.access_token || 'dummy-token';

        // Emit login success event with user data and token
        emit('login-success', userData, token);

        // Close the popup
        handleClose();
    } catch (error) {
        console.error('Login failed:', error);

        // Display error message
        if (error.response && error.response.data && error.response.data.message) {
            errorMessage.value = error.response.data.message;
        } else if (error.message) {
            errorMessage.value = error.message;
        } else {
            errorMessage.value = 'Failed to login. Please try again.';
        }
    } finally {
        isLoading.value = false;
    }
}
</script>

<style scoped>
/* You can add any additional styles here if needed */
</style>