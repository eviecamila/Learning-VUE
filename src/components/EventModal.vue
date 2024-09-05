<template>
    <generic-modal @close="closeModal">
        <swiper :slides-per-view="1" class="w-full h-2/4 mb-4 mt-8 max-h-64">
            <!-- Loop through the images -->
            <swiper-slide v-for="(image, index) in event.images" :key="index">
                <p class="px-2 text-center py-1 text-black font-bold text-xl bg-white rounded">🖼️{{
                    image.quoted
                }}
                </p>
                <img :src="image.image" class="rounded w-full h-full object-cover" alt="Event Image">

            </swiper-slide>
        </swiper>
        <!-- Event details -->
        <h2 class="text-xl text-black font-semibold mb-2">{{ event.title }}</h2>
        <p class="text-gray-700 mb-4">{{ event.description }}</p>
        <p class="text-gray-500">{{ event.details }}</p>
    </generic-modal>
</template>

<script lang="ts">
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/swiper-bundle.css';
import GenericModal from './Modal.vue';

export default {
    components: {
        Swiper,
        SwiperSlide,
        GenericModal
    },
    props: {
        event: {
            type: Object,
            required: true
        }
    },
    methods: {
        closeModal() {
            this.$emit('close');
        }
    }
};
</script>

<style scoped>
/* Add any additional styles for the content */
</style>
