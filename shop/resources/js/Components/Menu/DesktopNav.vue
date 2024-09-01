<template>
  <v-container fluid class="navbar">
    <v-row class="pb-3">
      <v-col cols="12">
        <!-- Desktop Links -->
        <v-row class="d-none d-md-flex  align-items-center justify-content-center " justify="start">
          <v-btn text class="category-btn categories-item" href="#all-categories">Категории <v-icon class="ml-2">mdi-menu</v-icon></v-btn>
          <v-btn text class="category-btn" href="#features">Лице</v-btn>
          <v-btn text class="category-btn" href="#makeup-beauty">Шминки</v-btn>
          <v-btn text class="category-btn" href="#contact-lenses">Тело</v-btn>
          <v-btn text class="category-btn" href="#personal-care-devices">Останато</v-btn>
        </v-row>

        <!-- Hamburger Menu for Mobile -->
        <v-row class="d-flex d-md-none" justify="end">
          <v-menu offset-y bottom left>
            <template v-slot:activator="{ on, attrs }">
              <v-btn icon v-bind="attrs" v-on="on">
                <v-icon>mdi-menu</v-icon>
              </v-btn>
            </template>

            <v-list>
              <v-list-item link href="#all-categories">
                <v-list-item-title>All Categories</v-list-item-title>
              </v-list-item>
              <v-list-item link href="#features">
                <v-list-item-title>Features</v-list-item-title>
              </v-list-item>
              <v-list-item link href="#makeup-beauty">
                <v-list-item-title>Makeup & Beauty</v-list-item-title>
              </v-list-item>
              <v-list-item link href="#contact-lenses">
                <v-list-item-title>Contact Lenses</v-list-item-title>
              </v-list-item>
              <v-list-item link href="#personal-care-devices">
                <v-list-item-title>Personal Care Devices</v-list-item-title>
              </v-list-item>
              <v-list-item link href="#others">
                <v-list-item-title>Others</v-list-item-title>
              </v-list-item>
            </v-list>
          </v-menu>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>
<style >
.navbar {
  background-color: #F9F4F0;
  padding: 0px;
}
.category-btn {
  font-weight: bold;
  text-transform: uppercase;
  font-size:14px;
  font-weight:bold;
  background:none;
  border:none;
  box-shadow:none;
  margin-left:15px;
}
.categories-item{
    background:#E5C1B1;
    margin-left:10px;
}
.category-btn:last-child {
  margin-right: 0; /* Remove the margin from the last button */
}

.v-menu {
  color: #A5674E; /* Mobile menu icon color */
}

.v-list-item-title {
  font-weight: bold;
  color: #A5674E; /* List item text color */
}
</style>
