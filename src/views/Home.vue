<script setup>
import { ref, onMounted, nextTick, watch } from "vue";
import HelloWorld from "../components/HelloWorld.vue";
import ChapterCard from "../components/ChapterCard.vue";
import ImageCarousel from "../components/ImageCarousel.vue";
import CreditSection from "../components/CreditSection.vue";
import axios from "axios";
import { useRouter } from 'vue-router';

const router = useRouter();

axios.defaults.baseURL = import.meta.env.VITE_API_BASE_URL + "/api"
axios.defaults.headers.common["Authorization"] = "Bearer 66tR3dHK19eZMR8qfvtvgFH7KBdmDsot2sk3iuyzyyTDRcvh6uY6iAOqk5MvQdtc"

// Search functionality
const searchQuery = ref('');
const searchResults = ref([]);
const isSearching = ref(false);
const showSearchResults = ref(false);

// Carousel images
const carouselImages = ref([
    "https://wsrv.nl/?url=cdn.meowing.org/uploads/v1Q1seEP3JV",
    "https://wsrv.nl/?url=cdn.meowing.org/uploads/v1Q1seEP3JV",
    "https://wsrv.nl/?url=cdn.meowing.org/uploads/v1Q1seEP3JV",
    "https://wsrv.nl/?url=cdn.meowing.org/uploads/v1Q1seEP3JV",
    "https://wsrv.nl/?url=cdn.meowing.org/uploads/v1Q1seEP3JV",
    "https://wsrv.nl/?url=cdn.meowing.org/uploads/v1Q1seEP3JV",
    "https://wsrv.nl/?url=cdn.meowing.org/uploads/v1Q1seEP3JV"
]);

const latestComics = ref([])
const isLoading = ref(true)

// Search function with debounce
let searchTimeout = null;
const performSearch = async () => {
  if (searchQuery.value.trim().length === 0) {
    searchResults.value = [];
    showSearchResults.value = false;
    return;
  }

  isSearching.value = true;
  
  try {
    const response = await axios.get(`/comics/search?q=${encodeURIComponent(searchQuery.value)}`);
    searchResults.value = response.data.data?.data || [];
    showSearchResults.value = true;
  } catch (error) {
    console.error("Search error:", error);
    searchResults.value = [];
  } finally {
    isSearching.value = false;
  }
};

// Watch for search input changes with debounce
watch(searchQuery, (newValue) => {
  clearTimeout(searchTimeout);
  if (newValue.trim().length === 0) {
    searchResults.value = [];
    showSearchResults.value = false;
    return;
  }
  
  searchTimeout = setTimeout(() => {
    performSearch();
  }, 300); // 300ms debounce
});

// Handle search submission
const handleSearchSubmit = () => {
  if (searchQuery.value.trim()) {
    router.push({ path: '/search', query: { q: searchQuery.value } });
    showSearchResults.value = false;
  }
};

// Close search results when clicking outside
const closeSearchResults = () => {
  setTimeout(() => {
    showSearchResults.value = false;
  }, 200);
};

// Navigate to comic
const navigateToComic = (comicId) => {
  router.push(`/comics/${comicId}`);
  showSearchResults.value = false;
  searchQuery.value = '';
};

onMounted(async () => {
    try {
        const response = await axios.get("/comics");
        console.log("API Response:", response.data.data);

        // Ensure we always have an array
        if (Array.isArray(response.data.data.data)) {
            latestComics.value = response.data.data.data;
        } else if (response.data.data.data && Array.isArray(response.data.data.data)) {
            latestComics.value = response.data.data.data;
        } else {
            console.warn("Unexpected API response format:", response.data);
            latestComics.value = [];
        }

        // Force a template update with nextTick
        await nextTick();
        console.log("After update, comic count:", latestComics.value.length);

        isLoading.value = false;
    } catch (error) {
        console.error("Error fetching comics:", error);
        isLoading.value = false;
    }

    // Add event listener to close search results when clicking outside
    document.addEventListener('click', (e) => {
      const searchContainer = document.getElementById('search-container');
      if (searchContainer && !searchContainer.contains(e.target)) {
        closeSearchResults();
      }
    });
});
</script>
<template>
    <div class="content px-8 md:px-12 lg:px-32 xl:px-48 py-4">
        <!-- Search Component - Desktop Version -->
        <div id="search-container" class="relative w-full mb-6 hidden md:block">
            <div class="flex flex-row gap-2 items-center">
                <div class="relative w-full max-w-2xl">
                    <input
                        v-model="searchQuery"
                        type="text"
                        placeholder="Search for comics..."
                        class="w-full bg-gray-200 px-4 py-2 rounded-full focus:outline-none focus:ring-2 focus:ring-gray-400"
                        @keyup.enter="handleSearchSubmit"
                    />
                    <div v-if="searchQuery.length > 0" class="absolute right-12 top-2.5">
                        <button @click="searchQuery = ''" class="text-gray-500 hover:text-gray-700">
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                <line x1="18" y1="6" x2="6" y2="18"></line>
                                <line x1="6" y1="6" x2="18" y2="18"></line>
                            </svg>
                        </button>
                    </div>
                    <button 
                        @click="handleSearchSubmit"
                        class="absolute right-3 top-2"
                    >
                        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                            <path d="M10 10m-7 0a7 7 0 1 0 14 0a7 7 0 1 0 -14 0" />
                            <path d="M21 21l-6 -6" />
                        </svg>
                    </button>
                    <!-- Search Results Dropdown -->
                    <div v-if="showSearchResults && searchQuery.length > 0" 
                        class="absolute top-full left-0 w-full mt-1 bg-white rounded-lg shadow-lg z-50 max-h-96 overflow-y-auto">
                        <div v-if="isSearching" class="p-4 text-center text-gray-500">
                            Searching...
                        </div>
                        <div v-else-if="searchResults.length === 0" class="p-4 text-center text-gray-500">
                            No results found
                        </div>
                        <div v-else>
                            <div v-for="result in searchResults" :key="result.id" 
                                class="p-2 hover:bg-gray-100 cursor-pointer flex items-center gap-3"
                                @click="navigateToComic(result.id)">
                                <img :src="result.image || 'https://wsrv.nl/?url=cdn.meowing.org/uploads/v1Q1seEP3JV'" 
                                    class="h-16 w-12 object-cover rounded" alt="" />
                                <div>
                                    <p class="font-medium">{{ result.name }}</p>
                                    <p class="text-sm text-gray-500">{{ result.type }}, {{ result.status }}</p>
                                </div>
                            </div>
                            <div class="p-2 border-t border-gray-200 text-center">
                                <button @click="handleSearchSubmit" class="text-blue-500 hover:text-blue-700">
                                    See all results
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Search Component - Mobile Version -->
        <div class="relative w-full mb-6 block md:hidden">
            <div class="flex flex-row gap-2 items-center">
                <div class="relative w-full">
                    <input
                        v-model="searchQuery"
                        type="text"
                        placeholder="Search for comics..."
                        class="w-full bg-gray-200 px-4 py-2 rounded-full focus:outline-none focus:ring-2 focus:ring-gray-400"
                        @keyup.enter="handleSearchSubmit"
                    />
                    <div v-if="searchQuery.length > 0" class="absolute right-12 top-2.5">
                        <button @click="searchQuery = ''" class="text-gray-500 hover:text-gray-700">
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                <line x1="18" y1="6" x2="6" y2="18"></line>
                                <line x1="6" y1="6" x2="18" y2="18"></line>
                            </svg>
                        </button>
                    </div>
                    <button 
                        @click="handleSearchSubmit"
                        class="absolute right-3 top-2"
                    >
                        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                            <path d="M10 10m-7 0a7 7 0 1 0 14 0a7 7 0 1 0 -14 0" />
                            <path d="M21 21l-6 -6" />
                        </svg>
                    </button>
                </div>
            </div>
            <!-- Mobile Search Results -->
            <div v-if="showSearchResults && searchQuery.length > 0" 
                class="absolute top-full left-0 w-full mt-1 bg-white rounded-lg shadow-lg z-50 max-h-96 overflow-y-auto">
                <div v-if="isSearching" class="p-4 text-center text-gray-500">
                    Searching...
                </div>
                <div v-else-if="searchResults.length === 0" class="p-4 text-center text-gray-500">
                    No results found
                </div>
                <div v-else>
                    <div v-for="result in searchResults" :key="result.id" 
                        class="p-2 hover:bg-gray-100 cursor-pointer flex items-center gap-3"
                        @click="navigateToComic(result.id)">
                        <img :src="result.image || 'https://wsrv.nl/?url=cdn.meowing.org/uploads/v1Q1seEP3JV'" 
                            class="h-16 w-12 object-cover rounded" alt="" />
                        <div>
                            <p class="font-medium">{{ result.name }}</p>
                            <p class="text-sm text-gray-500">{{ result.type }}, {{ result.status }}</p>
                        </div>
                    </div>
                    <div class="p-2 border-t border-gray-200 text-center">
                        <button @click="handleSearchSubmit" class="text-blue-500 hover:text-blue-700">
                            See all results
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <div class="image-carousel flex gap-4 justify-center items-center overflow-clip">
            <!-- <ImageCarousel :images="carouselImages" :autoplayDelay="3000" :imageWidth="160" /> -->
        </div>
        <CreditSection />
        <div class="grid grid-cols-7 gap-10 mt-8">
            <div class="col-span-5">
                <div class="latest-update">
                    <div class="flex justify-between items-center">
                        <p class="text-2xl font-semibold">Latest Update</p>
                        <a href="" class="text-lg">View all ></a>
                    </div>

                    <div v-if="isLoading" class="mt-2">
                        Loading comics...
                    </div>
                    <div v-else class="mt-2">
                        Comic count: {{ latestComics.length }}
                    </div>

                    <div v-if="isLoading" class="mt-6 text-center">
                        <p>Loading comics...</p>
                    </div>
                    <div v-else-if="latestComics.length === 0" class="mt-6 text-center">
                        <p>No comics found</p>
                    </div>
                    <div v-else class="grid grid-cols-3 gap-4 mt-6">
                        <div v-for="comic in latestComics" :key="comic.id">
                            <a :href="'/comics/' + comic.id"
                                class="bg-gray-50 ring-1 ring-gray-500/10 ring-inset rounded-lg flex items-center overflow-clip">
                                <img :src="comic.image || 'https://wsrv.nl/?url=cdn.meowing.org/uploads/v1Q1seEP3JV'"
                                    width="160" class="h-52" alt="">
                                <div class="flex flex-col px-4 w-100">
                                    <p class="text-lg font-semibold">{{ comic.name }}</p>
                                    <p class="text-sm text-gray-500">{{ comic.alternative_name }}</p>
                                    <div class="flex flex-wrap gap-1 mt-1">
                                        <span class="text-xs bg-gray-100 px-2 py-0.5 rounded">{{ comic.status }}</span>
                                        <span class="text-xs bg-gray-100 px-2 py-0.5 rounded">{{ comic.type }}</span>
                                    </div>
                                    <ul class="flex flex-col-reverse mt-3">
                                        <li
                                            class="py-1.5 px-1.5 flex justify-between rounded-lg transition-all duration-300 hover:bg-gray-100 hover:ring-1 hover:ring-gray-200 active:scale-95">
                                            <p class="text-sm">Chapter 1</p>
                                            <p class="text-sm">2 days ago</p>
                                        </li>
                                        <hr class="border-dashed border-gray-300">
                                        <li
                                            class="py-1.5 px-1.5 flex justify-between rounded-lg transition-all duration-300 hover:bg-gray-100 hover:ring-1 hover:ring-gray-200 active:scale-95">
                                            <p class="text-sm">Chapter 2</p>
                                            <p class="text-sm">4 days ago</p>
                                        </li>
                                        <hr class="border-dashed border-gray-300">
                                        <li
                                            class="py-1.5 px-1.5 flex justify-between rounded-lg transition-all duration-300 hover:bg-gray-100 hover:ring-1 hover:ring-gray-200 active:scale-95">
                                            <p class="text-sm">Chapter 3</p>
                                            <p class="text-sm">1 week ago</p>
                                        </li>
                                    </ul>
                                </div>
                            </a>
                        </div>
                    </div>
                </div>
                <div class="recently-added mt-8">
                    <div class="flex justify-between items-center">
                        <p class="text-2xl font-semibold">Recently Added</p>
                        <a href="" class="text-lg">View all ></a>
                    </div>
                    <div class="grid grid-cols-5 gap-4 mt-6">
                        <template v-if="latestComics && latestComics.length > 0">
                            <div v-for="(comic) in latestComics.slice(0, 5)" :key="'recent-' + comic.id"
                                class="flex flex-col items-center overflow-clip">
                                <a :href="'/comics/' + comic.id">
                                    <img :src="comic.image || 'https://wsrv.nl/?url=cdn.meowing.org/uploads/v1Q1seEP3JV'"
                                        width="160" class="w-100 rounded-lg" alt="">
                                    <p
                                        class="mt-2 text-lg font-semibold whitespace-nowrap overflow-hidden text-ellipsis w-full">
                                        {{ comic.name }}
                                    </p>
                                </a>
                            </div>
                        </template>
                        <div v-else class="col-span-5 text-center py-4">No comics available</div>
                    </div>
                </div>
            </div>
            <div class="col-span-2">
                <div class="flex justify-between items-center">
                    <p class="text-2xl font-semibold">Trending</p>
                </div>
                <div class="flex flex-col mt-6">
                    <div v-if="latestComics && latestComics.length > 0"
                        class="bg-gray-50 ring-1 ring-gray-500/10 rounded-lg ring-inset flex flex-col items-center overflow-clip">
                        <img :src="latestComics[0].image || 'https://wsrv.nl/?url=cdn.meowing.org/uploads/v1Q1seEP3JV'"
                            class="h-56 w-full object-cover" alt="">
                        <div class="flex gap-3 py-2 px-4 items-center w-full">
                            <p class="text-4xl font-bold">#1</p>
                            <div class="flex flex-col">
                                <p class="text-lg">{{ latestComics[0].name }}</p>
                                <span>{{ latestComics[0].type }}, {{ latestComics[0].status }}</span>
                            </div>
                        </div>
                    </div>
                    <div v-else class="text-center py-4 bg-gray-50 ring-1 ring-gray-500/10 rounded-lg">
                        No trending comics available
                    </div>
                </div>
            </div>
        </div>
        <div class="completed-series mt-8">
            <div class="flex justify-between items-center">
                <p class="text-2xl font-semibold">Completed Series</p>
                <a href="" class="text-lg">View all ></a>
            </div>
            <div class="grid grid-cols-6 gap-4 mt-6">
                <template v-if="latestComics && latestComics.length > 0">
                    <template v-for="comic in latestComics.filter(c => c.status === 'completed')"
                        :key="'completed-'+comic.id">
                        <div v-if="comic" class="flex flex-col items-center overflow-clip">
                            <img :src="comic.image || 'https://wsrv.nl/?url=cdn.meowing.org/uploads/v1Q1seEP3JV'"
                                width="160" class="w-100 rounded-lg" alt="">
                            <div class="flex flex-col self-start w-full items-start">
                                <p
                                    class="mt-2 text-lg font-semibold whitespace-nowrap overflow-hidden text-ellipsis w-full">
                                    {{ comic.name }}
                                </p>
                                <span class="w-full">{{ comic.comic_type }}, {{ comic.language }}</span>
                            </div>
                        </div>
                    </template>
                </template>
                <div v-else class="col-span-6 text-center py-4">No completed series available</div>
            </div>
        </div>
    </div>
</template>