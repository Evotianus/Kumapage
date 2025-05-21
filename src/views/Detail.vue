<script setup>
import ChapterCard from "../components/ChapterCard.vue";
import CommentSection from "../components/CommentSection.vue";
import CreditSection from "../components/CreditSection.vue";

import { ref, onMounted, watch } from 'vue';
import { useRoute } from 'vue-router';
import axios from 'axios';

axios.defaults.baseURL = import.meta.env.VITE_API_BASE_URL + "/api";
axios.defaults.headers.common["Authorization"] = "Bearer 66tR3dHK19eZMR8qfvtvgFH7KBdmDsot2sk3iuyzyyTDRcvh6uY6iAOqk5MvQdtc";

// State to track if the comic is in the library
const isInLibrary = ref(false);

// Function to toggle library status
const toggleLibraryStatus = () => {
    isInLibrary.value = !isInLibrary.value;
};

const route = useRoute();

const comicId = ref(route.params.comicId);
const comic = ref(null);

onMounted(() => {
    console.log('Comic ID:', comicId.value);

    try {
        axios.get(`/comics/${comicId.value}`)
            .then(response => {
                comic.value = response.data.data;
                console.log('Comic data:', comic.value);
            })
            .catch(error => {
                console.error('Error fetching comic data:', error);
            });
    } catch (error) {
        console.error('Error during mounted lifecycle:', error);
    }
    // You could fetch comic data based on this ID
    // fetchComicData(comicId.value);
});

// If you need to react to route parameter changes
// (useful for navigation between different comics without leaving the View component)
watch(() => route.params.comicId, (newId) => {
    comicId.value = newId;
    console.log('Comic ID changed to:', comicId.value);
    // fetchComicData(comicId.value);
});
</script>

<template>
    <div>
        <div class="content px-8 md:px-12 lg:px-32 xl:px-48 py-4">
            <div class="grid grid-cols-8 w-full gap-8">
                <div class="col-span-8 2xl:col-span-6">
                    <div class="comic-info lg:flex gap-8">
                        <div class="comic-cover w-fit">
                            <img v-if="comic" :src="comic.image" class="min-w-56 max-w-56 h-80 object-cover rounded-lg"
                                alt="">
                            <img v-else
                                src="https://assets.bwbx.io/images/users/iqjWHBFdfxIU/i3sY5OlfH3mc/v1/340x260.jpg"
                                class="min-w-56 max-w-56 h-80 object-cover rounded-lg" alt="">
                        </div>
                        <div class="comic-detail">
                            <h1 class="text-6xl font-bold">{{ comic ? comic.name : 'Loading...' }}
                            </h1>
                            <div class="detail-tags mt-4 flex gap-2">
                                <span
                                    class="inline-flex items-center rounded-md bg-green-50 px-2 py-1 text-sm font-medium text-green-700 ring-1 ring-green-600/20 ring-inset">{{
                                        comic ? comic.status : 'Loading...' }}</span>
                                <span
                                    class="inline-flex gap-2 items-center rounded-md bg-gray-50 px-2 py-1 text-sm font-medium text-gray-600 ring-1 ring-gray-500/10 ring-inset">
                                    <img src="https://imgs.search.brave.com/8cnLO-1k9cSqfKc0AzHje3mjsXrPbnKUdhwLUpx3FIc/rs:fit:500:0:0:0/g:ce/aHR0cHM6Ly9pbWcu/ZnJlZXBpay5jb20v/cHJlbWl1bS1waG90/by9mbGFnLWNoaW5h/LWNoaW5hLWZsYWct/Y2hpbmVzZS1mbGFn/XzEwNDMzNy0xMDIw/NS5qcGc_c2VtdD1h/aXNfaHlicmlk"
                                        class="w-5 h-5 object-cover object-left rounded-full" alt="">
                                    <span>{{ comic ? comic.comic_type : 'Loading...' }}</span>
                                </span>
                                <span
                                    class="inline-flex gap-2 items-center rounded-md bg-gray-50 px-2 py-1 text-sm font-medium text-gray-600 ring-1 ring-gray-500/10 ring-inset">
                                    <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24"
                                        fill="currentColor"
                                        class="icon icon-tabler icons-tabler-filled icon-tabler-clock-hour-4">
                                        <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                                        <path
                                            d="M17 3.34a10 10 0 1 1 -15 8.66l.005 -.324a10 10 0 0 1 14.995 -8.336m-5 2.66a1 1 0 0 0 -1 1v5.026l.009 .105l.02 .107l.04 .129l.048 .102l.046 .078l.042 .06l.069 .08l.088 .083l.083 .062l3 2a1 1 0 1 0 1.11 -1.664l-2.555 -1.704v-4.464a1 1 0 0 0 -.883 -.993z" />
                                    </svg>
                                    <span>{{ comic && comic.updated_at ? comic.updated_at : 'Feb 26, 2025' }}</span>
                                </span>
                                <span
                                    class="inline-flex gap-2 items-center rounded-md bg-gray-50 px-2 py-1 text-sm font-medium text-gray-600 ring-1 ring-gray-500/10 ring-inset">
                                    <span>{{ comic ? comic.language : 'Loading...' }}</span>
                                </span>
                            </div>
                            <div
                                class="detail-description mt-4 bg-gray-50 px-4 py-2 rounded-lg ring 1 ring-gray-500/10 ring-inset">
                                {{ comic ? comic.description : 'Loading...' }}
                                <br><br>
                                {{ comic ? comic.synopsis : 'Loading...' }}
                            </div>
                            <div class="flex flex-col md:flex-row h-full md:h-10 gap-2 mt-4">
                                <button
                                    class="px-3 py-2 bg-gray-50 ring-1 ring-gray-500/10 ring-inset rounded-lg flex justify-center items-center gap-2 transition-all duration-300 hover:bg-gray-100 hover:ring-gray-500/20 active:scale-95">
                                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                        fill="currentColor"
                                        class="icon icon-tabler icons-tabler-filled icon-tabler-player-play">
                                        <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                                        <path
                                            d="M6 4v16a1 1 0 0 0 1.524 .852l13 -8a1 1 0 0 0 0 -1.704l-13 -8a1 1 0 0 0 -1.524 .852z" />
                                    </svg>
                                    <span>Start Reading</span>
                                </button>
                                <button
                                    class="px-3 py-2 bg-gray-50 ring-1 ring-gray-500/10 ring-inset rounded-lg flex justify-center items-center gap-2 transition-all duration-300 hover:bg-gray-100 hover:ring-gray-500/20 active:scale-95">
                                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                        fill="currentColor"
                                        class="icon icon-tabler icons-tabler-filled icon-tabler-player-play">
                                        <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                                        <path
                                            d="M6 4v16a1 1 0 0 0 1.524 .852l13 -8a1 1 0 0 0 0 -1.704l-13 -8a1 1 0 0 0 -1.524 .852z" />
                                    </svg>
                                    <span>New Chapter</span>
                                </button>
                                <div
                                    class="vertical-divider mx-2 w-1 h-full rounded-full bg-gray-50 ring-1 ring-gray-500/10 ring-inset hidden md:block">
                                </div>
                                <div
                                    class="horizontal-divider my-1 rounded-full bg-gray-50 ring-1 ring-gray-500/10 ring-inset h-1 w-full block md:hidden">
                                </div>
                                <button
                                    class="add-to-library-btn px-10 py-2 bg-gray-50 ring-1 ring-gray-500/10 ring-inset rounded-lg flex justify-center items-center gap-2 transition-all duration-300 hover:bg-gray-100 hover:ring-gray-500/20 hover:shadow-sm active:scale-95"
                                    @click="toggleLibraryStatus">
                                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                        fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                        stroke-linejoin="round"
                                        :class="['icon transition-transform duration-300', isInLibrary ? 'text-green-600 rotate-45' : '']">
                                        <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                                        <path d="M12 5l0 14" />
                                        <path d="M5 12l14 0" />
                                    </svg>
                                    <span :class="{ 'text-green-600': isInLibrary }">{{ isInLibrary ? 'Added to Library'
                                        :
                                        'Add to Library' }}</span>
                                </button>
                                <button
                                    class="px-3 py-2 bg-gray-50 ring-1 ring-gray-500/10 ring-inset rounded-lg flex justify-center items-center gap-2 transition-all duration-300 hover:bg-gray-100 hover:ring-gray-500/20 active:scale-95">
                                    <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24"
                                        fill="currentColor"
                                        class="icon icon-tabler icons-tabler-filled icon-tabler-bell">
                                        <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                                        <path
                                            d="M14.235 19c.865 0 1.322 1.024 .745 1.668a3.992 3.992 0 0 1 -2.98 1.332a3.992 3.992 0 0 1 -2.98 -1.332c-.552 -.616 -.158 -1.579 .634 -1.661l.11 -.006h4.471z" />
                                        <path
                                            d="M12 2c1.358 0 2.506 .903 2.875 2.141l.046 .171l.008 .043a8.013 8.013 0 0 1 4.024 6.069l.028 .287l.019 .289v2.931l.021 .136a3 3 0 0 0 1.143 1.847l.167 .117l.162 .099c.86 .487 .56 1.766 -.377 1.864l-.116 .006h-16c-1.028 0 -1.387 -1.364 -.493 -1.87a3 3 0 0 0 1.472 -2.063l.021 -.143l.001 -2.97a8 8 0 0 1 3.821 -6.454l.248 -.146l.01 -.043a3.003 3.003 0 0 1 2.562 -2.29l.182 -.017l.176 -.004z" />
                                    </svg>
                                </button>
                            </div>
                        </div>
                    </div>
                    <CreditSection />
                    <div class="comic-episodes mt-6">
                        <div class="episodes-info flex justify-between items-center">
                            <p class="text-2xl font-semibold">100 Chapters</p>
                            <button>
                                <svg xmlns="http://www.w3.org/2000/svg" width="42" height="42" viewBox="0 0 24 24"
                                    fill="none" stroke="currentColor" stroke-width="1" stroke-linecap="round"
                                    stroke-linejoin="round"
                                    class="icon icon-tabler icons-tabler-outline icon-tabler-sort-descending-numbers">
                                    <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                                    <path d="M4 15l3 3l3 -3" />
                                    <path d="M7 6v12" />
                                    <path d="M17 14a2 2 0 0 1 2 2v3a2 2 0 1 1 -4 0v-3a2 2 0 0 1 2 -2z" />
                                    <path d="M17 5m-2 0a2 2 0 1 0 4 0a2 2 0 1 0 -4 0" />
                                    <path d="M19 5v3a2 2 0 0 1 -2 2h-1.5" />
                                </svg>
                            </button>
                        </div>
                        <div class="episodes-list grid grid-cols-3 gap-4 mt-6" v-if="comic != null">
                            <!-- <div class="bg-gray-50 ring-1 ring-gray-500/10 ring-inset rounded-lg p-2 flex items-center">
                                <div class="flex items-center gap-4">
                                    <img src="https://assets.bwbx.io/images/users/iqjWHBFdfxIU/ixfNTiyYtG1c/v0/459x306.webp"
                                        alt="" class="h-full w-36 rounded-lg">
                                    <div class="flex flex-col">
                                        <p class="font-semibold text-lg">Chapter 100</p>
                                        <span>Feb 27, 2025</span>
                                    </div>
                                </div>
                            </div> -->
                            <div v-for="section in comic.sections" :key="section.id">
                                    <a :href="'/comics' + '/' + comic.id + '/' + section.id">
                                    <ChapterCard :number="section.number" :date="section.updated_at" />
                                </a>
                                </div>
                        </div>
                    </div>
                    <CommentSection />
                </div>
                <div class="col-span-2 hidden 2xl:block">
                    <div class="other-comics">
                        <div
                            class="bg-gray-50 ring-1 ring-gray-500/10 ring-inset p-4 rounded-lg flex items-center gap-4">
                            <img v-if="comic" :src="comic.image" class="min-w-20 max-w-20 h-28 object-cover rounded-lg"
                                alt="">
                            <img v-else
                                src="https://assets.bwbx.io/images/users/iqjWHBFdfxIU/i3sY5OlfH3mc/v1/340x260.jpg"
                                class="min-w-20 max-w-20 h-28 object-cover rounded-lg" alt="">
                            <span class="text-3xl font-bold">1</span>
                            <div class="flex flex-col gap-2">
                                <p class="text-lg">{{ comic ? comic.name : 'Loading...' }}</p>
                                <span class="text-sm">{{ comic ? comic.comic_type : 'Loading...' }}</span>
                                <div class="flex flex-wrap gap-2">
                                    <span
                                        class="inline-block rounded-md bg-gray-50 px-2 py-1 text-sm font-medium text-gray-600 ring-1 ring-gray-500/10 ring-inset whitespace-nowrap">
                                        <span>{{ comic ? comic.language : 'Loading...' }}</span>
                                    </span>
                                    <span v-if="comic && comic.alternative_name"
                                        class="inline-block rounded-md bg-gray-50 px-2 py-1 text-sm font-medium text-gray-600 ring-1 ring-gray-500/10 ring-inset whitespace-nowrap">
                                        <span>{{ comic.alternative_name }}</span>
                                    </span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>