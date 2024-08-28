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
                <v-col cols="12" sm="12" lg="4" align="start">
                    <v-text-field
                        width="50%"
                        label="Shop Search"
                        placeholder="Search"
                        type="text"
                    ></v-text-field>
                </v-col>

                <v-col cols="4" align="center">
                    <div class="header_section--logo">
                        <img src="images/skin_boutique.png" />
                    </div>
                </v-col>

                <v-col cols="4" class="d-none d-md-block" align="center">
                    <div class="header_section--logo">
                        <img src="images/skin_boutique.png" />
                    </div>
                </v-col>
            </v-row>
        </v-container>
        <!-- Responsive Navbar -->
        <v-container fluid="true" class="navbar">
            <v-row align="center">
                <v-col cols="12">
                    <!-- Desktop Links -->
                    <v-row class="d-none d-md-flex" justify="center">
                        <v-btn text href="#home">Сите Категории</v-btn>
                        <v-btn class="ml-lg-5" text href="#shop">За Лице</v-btn>
                        <v-btn class="ml-lg-5" href="#about">За Тело</v-btn>
                        <v-btn class="ml-lg-5" href="#contact">Шминки</v-btn>
                        <v-btn class="ml-lg-5" text href="#contact">Колекции</v-btn>
                    </v-row>

                    <!-- Hamburger Menu -->
                    <v-row class="d-flex d-md-none" justify="end">
                        <v-menu offset-y bottom left>
                            <template v-slot:activator="{ on, attrs }">
                                <v-btn icon v-bind="attrs" v-on="on">
                                    <v-icon>mdi-menu</v-icon>
                                </v-btn>
                            </template>

                            <v-list>
                                <v-list-item link href="#home">
                                    <v-list-item-title>Home</v-list-item-title>
                                </v-list-item>
                                <v-list-item link href="#shop">
                                    <v-list-item-title>Shop</v-list-item-title>
                                </v-list-item>
                                <v-list-item link href="#about">
                                    <v-list-item-title>About</v-list-item-title>
                                </v-list-item>
                                <v-list-item link href="#contact">
                                    <v-list-item-title
                                        >Contact</v-list-item-title
                                    >
                                </v-list-item>
                            </v-list>
                        </v-menu>
                    </v-row>
                </v-col>
            </v-row>
        </v-container>
    </div>
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
    background: white !important;
    border-bottom: 2px solid #e4c1b1;
}
.navbar a{
    font-family: "Inter", sans-serif;
    font-optical-sizing: auto;
    font-weight: 600;
}
</style>
