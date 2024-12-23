<template>
  <v-container>
    <form @submit.prevent="handleSubmit">
      <v-text-field
        v-model.trim="state.email"
        :error-messages="v$.email.$errors.map(e => e.$message)"
        label="Seu E-mail"
        required
        @blur="v$.email.$touch"
        @input="v$.email.$touch"
      ></v-text-field>
      <v-text-field
        v-model.trim="state.code"
        :counter="10"
        :error-messages="v$.code.$errors.map(e => e.$message)"
        label="Insira o Código"
        required
        @blur="v$.code.$touch"
        @input="v$.code.$touch"
      ></v-text-field>
      <v-btn
        :disabled="overlay"
        :loading="overlay"
        class="me-4"
        type="submit"
      >
        Resgatar
      </v-btn>
    </form>
    <v-dialog v-model="dialogVisible" max-width="500">
      <template v-slot:default="">
        <v-card>
          <v-card-title class="headline">{{ dialogTitle }}</v-card-title>
          <v-card-text>{{ dialogMessage }}</v-card-text>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn text="Fechar" @click="dialogVisible = false">Fechar</v-btn>
          </v-card-actions>
        </v-card>
      </template>
    </v-dialog>
    <v-overlay v-model="overlay" persistent scroll-strategy="none"></v-overlay>
  </v-container>
</template>

<script lang="ts" setup>
import {reactive} from 'vue';
import {useVuelidate} from '@vuelidate/core';
import {email, required} from '@vuelidate/validators';

const initialState = {
  code: '',
  email: '',
}

const state = reactive({
  ...initialState,
})

const rules = {
  code: {required},
  email: {required, email},
}

const v$ = useVuelidate(rules, state);

const dialogVisible = ref(false);
const dialogTitle = ref('');
const dialogMessage = ref('');
const overlay = ref(false);

const handleSubmit = async () => {
  const isValid = await v$.value.$validate();
  if (!isValid) {
    dialogTitle.value = 'Erro';
    dialogMessage.value = 'Por favor, preencha os campos corretamente.';
    dialogVisible.value = true;
    return;
  }
  overlay.value = true;
  setTimeout(() => {
    overlay.value = false;
    dialogTitle.value = 'Sucesso';
    dialogMessage.value = 'Premiação enviada a conta do e-mail com sucesso!';
    dialogVisible.value = true;
  }, 2000);
};
</script>

<style scoped>

</style>
