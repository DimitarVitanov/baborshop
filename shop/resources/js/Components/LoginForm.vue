<script setup>
import { ref } from "vue";

const currentStep = ref(0); // Manually track the current step
const show_alert = ref(false)
const alert_message = ref('')
const user = ref({
    name: null,
    surname: null,
    email: null,
    password: null,
});

const next = () => {
    if (currentStep.value < 3) {
        currentStep.value++;
    }
};

const prev = () => {
    if (currentStep.value > 0) {
        currentStep.value--;
    }
};


const complete = () => {
    currentStep.value++;
    checkValidity()
};
const checkValidity = () => {
    if(!user.value.name || user.value.name == ''){
        alert_message.value = 'Ве молиме, пополнето го вашето име'
        show_alert.value=true
        currentStep.value=0
    }
    else if(!user.value.surname || user.value.surname == ''){
        alert_message.value = 'Ве молиме, пополнето го вашето презиме'
        show_alert.value=true
        currentStep.value=1
    }
    else if(!user.value.email || user.value.email == '' || !user.value.email.includes('@')){
        alert_message.value = 'Ве молиме, пополнето ја вашата е-пошта'
        show_alert.value=true
        currentStep.value=2
    }
    else if(!user.value.password || user.value.password == ''){
        alert_message.value = 'Вашата лозинка не може да биде празна'
        show_alert.value=true
        currentStep.value=3
    }else{
        saveCredentials()
    }
}
const saveCredentials = () => {

}
</script>

<template>
    <v-stepper  hide-actions v-model="currentStep" alt-labels non-linear>
        <v-stepper-header class="d-none d-md-flex" >
            <v-stepper-item :complete="currentStep > 0" icon="mdi mdi-account" title="Име" value="0">
            </v-stepper-item>
            <v-stepper-item :complete="currentStep > 1" icon="mdi mdi-account" title="Презиме" value="1">
            </v-stepper-item>
            <v-stepper-item :complete="currentStep > 2" icon="mdi mdi-email-box" title="Е-пошта" value="2">
            </v-stepper-item>
            <v-stepper-item :complete="currentStep > 3" icon="mdi mdi-lock-check" title="Лозинка" value="3">
            </v-stepper-item>
             <v-stepper-item :complete="currentStep > 4" class="d-none" icon="mdi mdi-lock-check" title="Лозинка" value="3">
            </v-stepper-item>
        </v-stepper-header>

        <v-stepper-window direction="vertical">
         <v-alert icon="$error" v-model="show_alert" color="error">
         <h4>Настана грешка</h4>
         <p>{{ alert_message }}</p>
         </v-alert>
            <v-stepper-window-item value="0">
                <v-card title="Вашето име" flat>
                    <v-text-field
                        @input="()=>{show_alert = false}"
                        v-model="user.name"
                        label="Име"
                        placeholder="Вашето име"
                        outlined
                    ></v-text-field>
                </v-card>
            </v-stepper-window-item>
            <v-stepper-window-item value="1">
                <v-card title="Вашето презиме" flat>
                    <v-text-field
                        v-model="user.surname"
                         @input="()=>{show_alert = false}"
                        label="Презиме"
                        icon="fa fa-person"
                        placeholder="Вашето презиме"
                        outlined
                    ></v-text-field>
                </v-card>
            </v-stepper-window-item>

            <v-stepper-window-item value="2">
                <v-card title="Вашата е-пошта" flat>
                    <v-text-field
                        v-model="user.email"
                        @input="()=>{show_alert = false}"
                        label="Е-Пошта"
                        placeholder="Вашата е-пошта"
                        outlined
                        type="email"
                    ></v-text-field>
                </v-card>
            </v-stepper-window-item>

            <v-stepper-window-item value="3">
                <v-card title="Вашата лозинка" flat>
                    <v-text-field
                        v-model="user.password"
                         @input="()=>{show_alert = false}"
                        label="Лозинка"
                        placeholder="Внесете ја вашата лозинка"
                        outlined
                        type="password"
                    ></v-text-field>
                </v-card>
            </v-stepper-window-item>
        </v-stepper-window>
        <v-stepper-actions v-if="currentStep <= 3">
            <template v-if="currentStep == 3" #next="{ props }" disabled='false'>
                <v-btn  @click="complete()">Регистрирај се</v-btn>
            </template>
            <template v-else #next="{ props }">
                <v-btn @click="next()">Напред</v-btn>
            </template>
            <template #prev="{ props }">
                <v-btn @click="prev()">Назад</v-btn>
            </template>
        </v-stepper-actions>
    </v-stepper>
</template>

<style scoped>
/* You can add custom styles here */
</style>
