<script setup>
import { useDisplay } from "vuetify";
import { ref,computed } from "vue";

const slides = ref([
    "/images/slider/hsr_slider.png",
    "/images/skin_boutique.png",
]);

const { smAndDown } = useDisplay();
const carouselHeight = computed(()=>{
    return smAndDown.value ? 'auto' : '73vh';
})
</script>

<template>
  <div class="home">
        <v-carousel
            background="#FCF7F4"
            :height="carouselHeight"
            hide-delimiters
        >
            <v-carousel-item v-for="(slide, i) in slides" :key="i">
                <v-sheet height="100%">
                    <div class="d-flex fill-height justify-center align-center">
                        <v-img cover
                            :src="slide"
                            alt="Slide image"
                            height="100%"
                            width="100%"
                            class="responsive-img image-background-color"
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
}
.image-background-color{
    background:#FCF7F4;
}
</style>
