<script setup>
import { ref } from "vue";

const user = ref({
  name: null,
  surname: null,
  email: null,
  password: null,
});

</script>

<template>
  <v-stepper :items="['Име', 'Презиме', 'Е-Пошта', 'Лозинка']">
    <template v-slot:item.1>
      <v-card title="Внесете го вашето име" flat>
        <v-text-field
          v-model="user.name"
          label="Име"
          placeholder="Внесете го вашето име"
          outlined
        ></v-text-field>
      </v-card>
    </template>

    <template v-slot:item.2>
      <v-card title="Внесете го вашето презиме" flat>
        <v-text-field
          v-model="user.surname"
          label="Презиме"
          placeholder="Внесете го вашето презиме"
          outlined
        ></v-text-field>
      </v-card>
    </template>

    <template v-slot:item.3>
      <v-card title="Вашата електронска пошта" flat>
        <v-text-field
          v-model="user.email"
          label="Е-Пошта"
          placeholder="Внесете ја вашата е-пошта"
          outlined
          type="email"
        ></v-text-field>
      </v-card>
    </template>

    <template v-slot:item.4>
      <v-card title="Вашата лозинка" flat>
        <v-text-field
          v-model="user.password"
          label="Лозинка"
          placeholder="Внесете ја вашата лозинка"
          outlined
          type="password"
        ></v-text-field>
      </v-card>
    </template>
  </v-stepper>
</template>

<style scoped>
/* You can add custom styles here */
</style>
