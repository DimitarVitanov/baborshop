<script setup>
import { ref, onMounted } from "vue";
import LoginForm from "@/Components/LoginForm.vue"
import DesktopNav from "@/Components/Menu/DesktopNav.vue"
const show_form_modal = ref(false)
const selected_user = ref(null)

onMounted(()=>{
    selected_user.value = document.querySelector('meta[name="user"]') ? JSON.parse(document.querySelector('meta[name="user"]').getAttribute('content')) : null
})

const openOptionModal = () =>{
    show_option_modal.value = true
}
const openFormModal = () => {
    show_form_modal.value = true;
}

const menu_items = [
    { title: 'Macedonian' },
    { title: 'English' },
]
</script>
<template>
    <header>
        <v-container>
            <v-row>
                <v-col cols="12" class="py-1">
                    <p>Безплатен достава на сите нарачки над 2000денари</p>
                </v-col>
            </v-row>
        </v-container>
    </header>
    <div class="header_section">
        <v-container fluid="true">
            <v-row align="center">
                <v-col cols="12" sm="12" lg="4" class="d-none d-md-block" align="start">
                    <v-text-field width="50%" label="Shop Search" placeholder="Search" type="text"></v-text-field>
                </v-col>

                <v-col cols="12" sm="12" lg="4" align="center">
                    <div class="header_section--logo">
                        <img src="images/skin_boutique.png" />
                    </div>
                </v-col>

                <v-col cols="12" sm="12" lg="4" align="center">
                    <div class="d-flex align-center justify-center">
                        <div @click="!selected_user ? openFormModal() : $inertia.visit(route('dashboard'))"
                            class="header_section--account d-flex align-center justify-center ml-8 cursor-pointer">
                            <v-icon size="30" icon="mdi mdi-account-circle" class="my-0 py-0" />
                            <small v-if="!selected_user" class="text-uppercase ml-2">Your account</small>
                            <small v-else class="text-uppercase ml-2"> {{ selected_user.name }}</small>
                        </div>
                        <div class="d-flex  ml-8 ">
                            <v-icon size="30" icon="mdi mdi-cart-outline" class="my-0 py-0" />
                            <div class="header_section--card d-flex flex-column ml-1">
                                <small>Кошничка</small>
                                <small>0.00 ден.</small>
                            </div>

                            <div class="ml-8">
                                <v-menu transition="slide-x-transition">
                                    <template v-slot:activator="{ props }">
                                        <v-icon size="30" color="#e4c1b1" v-bind="props" icon="mdi mdi-earth-arrow-down"
                                            class="my-0 py-0" />
                                    </template>

                                    <v-list>
                                        <v-list-item v-for="(item, i) in menu_items" :key="i">
                                            <v-list-item-title>{{ item.title }}</v-list-item-title>
                                        </v-list-item>
                                    </v-list>
                                </v-menu>
                            </div>
                        </div>
                    </div>

                </v-col>

            </v-row>
        </v-container>
        <!-- Responsive Navbar -->
        <DesktopNav/>
    </div>


    <!--start:: Login Form Modal -->
        <v-dialog max-width="800" v-model="show_form_modal">
            <LoginForm />
        </v-dialog>
    <!--end:: Login Form Modal-->
</template>

<style>
header {
    font-size: 0.8rem;
    text-align: center;
    background: #e4c1b1;
    font-family: "Inter", sans-serif;
    font-optical-sizing: auto;
    font-weight: 300;
    font-style: normal;
}

.header_section {
    width: 100%;
}

.header_section img {
    width: 200px;
    height: 130px;
}

.v-field__field {
    border: none !important;
    background: #ffffff !important;
    border-bottom: 2px solid #e4c1b1;
}

.navbar a {
    font-family: "Inter", sans-serif;
    font-optical-sizing: auto;
    font-weight: 600;
}

.header_section--card small {
    font-size: 10px;
    margin: 0px;
    padding: 0px;
    font-family: "Inter", sans-serif;
    font-optical-sizing: auto;
    font-weight: 600;
}

.header_section--card small:last-child {
    font-weight: 800;
}

.header_section--account {
    font-family: "Inter", sans-serif;
    font-optical-sizing: auto;
    font-weight: 800;
}

.header_section--account small {
    font-size: 10px;
}
</style>
