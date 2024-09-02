<script setup>
import { ref } from "vue";
import {Head} from '@inertiajs/vue3'
const currentStep = ref(0); // Manually track the current step
const show_registration_form = ref(false)
const show_login_form = ref(false)
const alert_message = ref('')
const user = ref({
    name: null,
    surname: null,
    email: null,
    password: null,
    password_confirmation:null,
});
const fireMessage = (message, success = false, reload = false, route = null)=>{
    Swal.fire({
        position: 'top',
        title: message,
        icon: success ? 'success' : 'error',
        toast: true,
        showConfirmButton:false,
        timer:2000,
    }).then(()=>{
        if(reload){
            location.reload()
        }else if(route){
            window.location.href = `${window.location.origin}/${route}`;
        }
    })
}
const handleRegistrationStep = () => {
    currentStep.value = 0;
    show_registration_form.value = true;
}
const handleLoginStep = () =>{
    show_login_form.value = true
}
const goBackToOption = () =>{
    show_login_form.value= false
    show_registration_form.value = false
    currentStep.value = 0
}
const clearValues = ()=>{
    show_registration_form = false
    show_login_form = false
    user.value.name = null
    user.value.surname = null
    user.value.email = null
    user.value.password = null
}
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
    //currentStep.value++;
    checkValidity()
};
const checkValidity = () => {
    if(show_registration_form){
    if(!user.value.name || user.value.name == ''){
        fireMessage('Ве молиме, пополнето го вашето име')
        currentStep.value=0
        return
    }
    else if(!user.value.surname || user.value.surname == ''){
        fireMessage('Ве молиме, пополнето го вашето презиме')
        currentStep.value=1
        return
    }
    else if(!user.value.email || user.value.email == '' || !user.value.email.includes('@')){
        fireMessage('Ве молиме, пополнето ја вашата е-пошта')
        currentStep.value=2
        return
    }
    else if(!user.value.password || user.value.password == ''){
        fireMessage('Вашата лозинка не може да биде празна')
        currentStep.value=3
        return
    }else if(user.value.password != user.value.password_confirmation){
        fireMessage('Двете лозинки не се исти')
        currentStep.value=3
        return
    }
     saveCredentials()
    }
    else {
     checkCredentials()
    }
}
const saveCredentials = async() => {
    const formData =new FormData();
    const csrfToken = document.querySelector('meta[name="csrf-token"]').getAttribute('content');
    formData.append('_token', csrfToken)
    formData.append('name', user.value.name + ' ' + user.value.surname)
    formData.append('email', user.value.email)
    formData.append('password', user.value.password)
    formData.append('password_confirmation', user.value.password_confirmation)


    const response = await fetch(route('register'),{
        method:'POST',
        body:formData,
    })
    if (response.ok) {
    fireMessage('Успешна регистрација!', true, false, 'dashboard');
    } else {
    fireMessage('Регистрацијата не успеа. Ве молиме, обидете се повторно.');
    }
    clearValues()
}

const checkCredentials = async ()=>{
    try{
    const formData = new FormData()
    const csrfToken = document.querySelector("meta[name='csrf-token']").getAttribute('content')
    formData.append('_token', csrfToken)
    formData.append('email', user.value.email)
    formData.append('password', user.value.password)
    formData.append('remember', false)

    const response = await fetch(route('login'),{
        method:'POST',
        body:formData
    })
    if (!response.ok) {
            throw new Error('Failed to authenticate');
    }
    const data = await response.json();

    if (data.success) {
        fireMessage('Успешно се најавивте', true, false, 'dashboard');
    } else {
        fireMessage( 'Настана грешка, ве молиме обидете се повтроно.', false);
    }
}catch(error){
    console.error(error)
    fireMessage('Настана грешка, ве молиме обидете се повтроно.', false);
}
}
</script>

<template>
        <GuestLayout>
            <Head title="Register Form" />
    <v-stepper  hide-actions v-model="currentStep" alt-labels non-linear>
        <v-stepper-header class="d-none d-md-flex" >
        <!-- Adjust visibility based on show_registration_form -->
        <v-stepper-item :complete="currentStep > 10" v-if="!show_registration_form && !show_login_form" icon="mdi mdi-account" class="mx-auto" title="Избор" value="10"></v-stepper-item>
        <v-stepper-item :complete="currentStep > 11" v-if="show_login_form" icon="mdi mdi-account" title="Влез" value="11" class="mx-auto"></v-stepper-item>
        <v-stepper-item :complete="currentStep > 0" v-if="show_registration_form" icon="mdi mdi-account" title="Име" value="0"></v-stepper-item>
        <v-stepper-item :complete="currentStep > 1" v-if="show_registration_form" icon="mdi mdi-account" title="Презиме" value="1"></v-stepper-item>
        <v-stepper-item :complete="currentStep > 2" v-if="show_registration_form" icon="mdi mdi-email-box" title="Е-пошта" value="2"></v-stepper-item>
        <v-stepper-item :complete="currentStep > 3" v-if="show_registration_form" icon="mdi mdi-lock-check" title="Лозинка" value="3"></v-stepper-item>
        <v-stepper-item v-if="show_registration_form" class='d-none' icon="mdi mdi-lock-check" title="Лозинка" value="3"></v-stepper-item>

    </v-stepper-header>

        <v-stepper-window direction="vertical">
            <v-stepper-window-item value="10" v-if="!show_registration_form && !show_login_form">
                <v-card title="Ве молиме изберете" flat>
                        <v-btn @click="handleLoginStep()" color="primary" class="ml-2 mt-2"> Логирај се</v-btn>
                        <v-btn @click="handleRegistrationStep()" color="red" class="ml-2 mt-2 "> Регистрирај се</v-btn>
                </v-card>
            </v-stepper-window-item>
            <v-stepper-window-item value="11" v-if="show_login_form">
                <v-card flat>

                    <div class="d-flex flex-column mb-4">
                        <p class="mb-2 text-center">
                        Логирај се со
                    </p>
                    <v-btn color="red" class="w-50 mx-auto">Google</v-btn>
                    <v-btn color="primary" class="w-50 mx-auto mt-2">Facebbok</v-btn>
                    </div>
                    <v-text-field
                        v-model="user.email"
                        label="Корисничко име или емаил"
                        placeholder="Корисничко име"
                        outlined
                        type="email"
                    ></v-text-field>
                    <v-text-field
                        v-model="user.password"
                        label="Лозинка"
                        placeholder="Вашата лозинка"
                        outlined
                        type="password"
                    ></v-text-field>
                    <div class="d-flex justify-between">
                        <v-btn @click="goBackToOption()"color="gray">Назад</v-btn>
                        <v-btn color="success" @click="checkCredentials()" class="mb-2">Логирај се</v-btn>
                    </div>
                    

                </v-card>
            </v-stepper-window-item>

            <v-stepper-window-item value="0">
                <v-card title="Вашето име" flat>
                    <v-text-field
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
                        label="Лозинка"
                        placeholder="Внесете ја вашата лозинка"
                        outlined
                        type="password"
                    ></v-text-field>

                    <v-text-field
                        v-model="user.password_confirmation"
                        label="Повторете ја вашата лозинка"
                        placeholder="Повторете ја вашата лозинка"
                        outlined
                        type="password"
                    ></v-text-field>
                </v-card>
            </v-stepper-window-item>
        </v-stepper-window>
        <v-stepper-actions :class="show_registration_form ? 'd-flex' : 'd-none'" v-if="currentStep <= 3">
            <template v-if="currentStep == 3" #next="{ props }" disabled='false'>
                <v-btn  @click="complete()">Регистрирај се</v-btn>
            </template>
            <template v-else #next="{ props }">
                <v-btn @click="next()">Напред</v-btn>
            </template>
            <template #prev="{ props }">
                <v-btn v-if="currentStep > 0" @click="prev()">Назад</v-btn>
                <v-btn v-else :disabled="false" color="gray" @click="goBackToOption">Назад</v-btn>
            </template>
        </v-stepper-actions>
    </v-stepper>
    </GuestLayout>
</template>

<style>
.swal2-container{
    z-index: 9999;
}
.v-text-field input[type='text']:focus,
.v-text-field input[type='password']:focus,
.v-text-field input[type='email']:focus 
{
  outline: none;
  border-color: transparent;
  box-shadow: none;
}
</style>
