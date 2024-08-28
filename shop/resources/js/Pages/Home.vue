<script setup>
import Header from "@/Components/Header.vue";
import { ref,computed } from "vue";
import { useDisplay } from "vuetify";

const slides = ref([
    "/images/slider/hsr_slider.png",
    "/images/skin_boutique.png",
]);
const { smAndDown } = useDisplay();
const carouselHeight = computed(()=>{
    return smAndDown.value ? 'auto' : '65vh';
})

</script>

<template>
    <Header />
    <div class="home pt-md-5">
        <v-carousel
            class="py-md-5"
            :height="carouselHeight"
            progress="#E4C1B1"
            hide-delimiters
        >
            <v-carousel-item v-for="(slide, i) in slides" :key="i">
                <v-sheet height="100%">
                    <div class="d-flex fill-height justify-center align-center">
                        <v-img
                            :src="slide"
                            alt="Slide image"
                            height="100%"
                            width="100%"
                            class="responsive-img"
                        />
                    </div>
                </v-sheet>
            </v-carousel-item>
        </v-carousel>
    </div>
</template>

<style>
.home {
    width: 100%;
    height: 100vh;
}
</style>
