<script setup>
import Header from "@/Components/Header.vue";
import { ref } from "vue";
const slides = ref(["images/skin_boutique.png", "images/skin_boutique.png"]);
</script>
<template>
    <Header />
    <div class="home">
        <v-carousel height="60vh" progress="#E4C1B1" hide-delimiters>
            <v-carousel-item v-for="(slide, i) in slides" :key="i">
                <v-sheet height="100%">
                    <div class="d-flex fill-height justify-center align-center">
                        <v-img
                            :src="slide"
                            alt="Slide image"
                            height="100%"
                            width="100%"
                            contain
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
