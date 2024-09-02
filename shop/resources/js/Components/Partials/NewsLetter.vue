<template>
    <div class="news_letter">
    <v-container>
        <v-row>
            <v-col cols="12" sm="12" md="6" class="mx-auto">

                <h2 class="text-center text-uppercase">Our newsletter</h2>
                <div class="d-flex mt-3">
                    <v-text-field
                        color=""
                        density="compact"
                        placeholder="Enter your email address"
                        prepend-inner-icon="mdi-email-outline"
                        variant="outlined"
                    ></v-text-field>
                    <v-btn color="black" class="ml-2 subscribe-btn">Subscribe</v-btn>
                </div>

            </v-col>
        </v-row>
    </v-container>
    </div>
</template>

<style>
.news_letter{
    padding:4rem 0;
    background: #FBF6F4;
}
.news_letter h2{
    font-size:1.4rem;
    font-weight: bold;
}
.v-text-field input[type='text']:focus {
  outline: none;
  border-color: transparent;
  box-shadow: none;
}
.subscribe-btn{
    margin-top:1.5px
}

</style>