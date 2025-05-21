<script setup>
import { ref, onMounted, onBeforeUnmount, computed, reactive } from 'vue';

const props = defineProps({
    images: {
        type: Array,
        default: () => [
            "https://wsrv.nl/?url=cdn.meowing.org/uploads/v1Q1seEP3JV",
            "https://wsrv.nl/?url=cdn.meowing.org/uploads/v1Q1seEP3JV",
            "https://wsrv.nl/?url=cdn.meowing.org/uploads/v1Q1seEP3JV",
            "https://wsrv.nl/?url=cdn.meowing.org/uploads/v1Q1seEP3JV",
            "https://wsrv.nl/?url=cdn.meowing.org/uploads/v1Q1seEP3JV",
            "https://wsrv.nl/?url=cdn.meowing.org/uploads/v1Q1seEP3JV",
            "https://wsrv.nl/?url=cdn.meowing.org/uploads/v1Q1seEP3JV"
        ]
    },
    autoplayDelay: {
        type: Number,
        default: 3000
    },
    imageWidth: {
        type: Number,
        default: 160
    },
    imagesDisplayed: {
        type: Number,
        default: 5
    }
});

const currentIndex = ref(0);
const isAutoplay = ref(true);
const autoplayInterval = ref(null);
const touchStartX = ref(0);
const containerRef = ref(null);
const translateX = ref(0);
const imagesPerView = ref(props.imagesDisplayed);

// Calculate the translate value based on currentIndex
const updateTranslateX = () => {
    const width = props.imageWidth + 16; // image width + gap
    translateX.value = -currentIndex.value * width;
};

const nextSlide = () => {
    if (currentIndex.value < props.images.length - imagesPerView.value) {
        currentIndex.value++;
    } else {
        currentIndex.value = 0; // Reset to beginning when reaching the end
    }
    updateTranslateX();
};

const prevSlide = () => {
    if (currentIndex.value > 0) {
        currentIndex.value--;
    } else {
        currentIndex.value = props.images.length - imagesPerView.value; // Go to end when at beginning
        if (currentIndex.value < 0) currentIndex.value = 0; // Ensure we don't go negative
    }
    updateTranslateX();
};

const goToSlide = (index) => {
    if (index >= 0 && index <= props.images.length - imagesPerView.value) {
        currentIndex.value = index;
        updateTranslateX();
    }
};

const startAutoplay = () => {
    if (!isAutoplay.value) return;

    stopAutoplay();
    autoplayInterval.value = setInterval(() => {
        nextSlide();
    }, props.autoplayDelay);
};

const stopAutoplay = () => {
    if (autoplayInterval.value) {
        clearInterval(autoplayInterval.value);
        autoplayInterval.value = null;
    }
};

const handleMouseEnter = () => {
    stopAutoplay();
};

const handleMouseLeave = () => {
    startAutoplay();
};

const handleTouchStart = (e) => {
    touchStartX.value = e.touches[0].clientX;
    stopAutoplay();
};

const handleTouchEnd = (e) => {
    const touchEndX = e.changedTouches[0].clientX;
    const diff = touchStartX.value - touchEndX;

    // Swipe detection
    if (Math.abs(diff) > 50) { // Minimum swipe distance
        if (diff > 0) {
            nextSlide();
        } else {
            prevSlide();
        }
    }

    startAutoplay();
};

const calculateVisibleImages = () => {
    if (!containerRef.value) return;

    const containerWidth = containerRef.value.clientWidth;
    // Calculate how many images can fit in the container
    const itemWidth = props.imageWidth + 16; // width + gap
    const calculated = Math.floor(containerWidth / itemWidth);

    imagesPerView.value = Math.min(calculated, props.images.length);
    if (imagesPerView.value < 1) imagesPerView.value = 1;

    // Make sure currentIndex is valid with new imagesPerView
    if (currentIndex.value > props.images.length - imagesPerView.value) {
        currentIndex.value = Math.max(0, props.images.length - imagesPerView.value);
    }

    updateTranslateX();
};

const handleResize = () => {
    calculateVisibleImages();
};

// Check if indicator should be active
const isActiveIndicator = (index) => {
    return index >= currentIndex.value && index < currentIndex.value + imagesPerView.value;
};

onMounted(() => {
    calculateVisibleImages();
    startAutoplay();
    window.addEventListener('resize', handleResize);
});

onBeforeUnmount(() => {
    stopAutoplay();
    window.removeEventListener('resize', handleResize);
});
</script>

<template>
    <div class="carousel-container relative" @mouseenter="handleMouseEnter" @mouseleave="handleMouseLeave"
        @touchstart="handleTouchStart" @touchend="handleTouchEnd" ref="containerRef">
        <div class="carousel-controls absolute inset-y-0 left-0 flex items-center">
            <button @click.prevent="prevSlide"
                class="carousel-prev bg-black/30 hover:bg-black/50 text-white rounded-full p-2 z-10">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                    stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                    class="w-6 h-6">
                    <path d="M15 18l-6-6 6-6" />
                </svg>
            </button>
        </div>

        <div class="carousel-track overflow-hidden">
            <div class="carousel-content flex gap-4 transition-transform duration-300"
                :style="{ transform: `translateX(${translateX}px)` }">
                <div v-for="(image, idx) in props.images" :key="idx" class="carousel-item flex-shrink-0">
                    <img :src="image" :alt="`Carousel image ${idx + 1}`" :width="props.imageWidth" class="rounded-lg">
                </div>
            </div>
        </div>

        <div class="carousel-controls absolute inset-y-0 right-0 flex items-center">
            <button @click.prevent="nextSlide"
                class="carousel-next bg-black/30 hover:bg-black/50 text-white rounded-full p-2 z-10">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                    stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                    class="w-6 h-6">
                    <path d="M9 18l6-6-6-6" />
                </svg>
            </button>
        </div>

        <div class="carousel-indicators flex justify-center gap-2 mt-4">
            <button v-for="i in props.images.length - imagesPerView.value + 1" :key="i - 1" @click="goToSlide(i - 1)"
                class="w-2 h-2 rounded-full transition-colors duration-300"
                :class="currentIndex === i - 1 ? 'bg-blue-500' : 'bg-gray-300'">
            </button>
        </div>
    </div>
</template>

<style scoped>
.carousel-container {
    position: relative;
    width: 100%;
    overflow: hidden;
}

.carousel-track {
    width: 100%;
    overflow: hidden;
}

.carousel-content {
    will-change: transform;
}

.carousel-controls button {
    opacity: 0;
    transition: opacity 0.3s ease;
}

.carousel-container:hover .carousel-controls button {
    opacity: 1;
}
</style>