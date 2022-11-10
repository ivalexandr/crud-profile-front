<template>
  <q-form class="form" @submit="submitHandler">
    <q-input
      rounded
      outlined
      clearable
      type="email"
      v-model="email"
      label="Email"
      name="email"
      hint="email"
      lazy-rules
      :rules="[(val) => (val && val.length > 0) || 'Field is required']"
    >
      <template v-slot:append>
        <q-icon name="email" />
      </template>
    </q-input>
    <q-input
      rounded
      outlined
      clearable
      type="password"
      v-model="password"
      label="Password"
      hint="password"
      lazy-rules
      :rules="[(val) => val.length >= 6 || 'Must be at least 6 characters']"
    >
      <template v-slot:append>
        <q-icon name="password" />
      </template>
    </q-input>
    <q-btn outline rounded type="submit" color="purple">
      {{ buttonText }}
    </q-btn>
  </q-form>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { TBody } from './types';
import { AxiosError } from 'axios';
import { useQuasar } from 'quasar';
import { api } from 'src/boot/axios';
import { ref } from 'vue';

export default defineComponent({
  name: 'AuthForm',
  setup() {
    //eslint-disable-next-line
    const $q = useQuasar();
    return {
      email: ref(''),
      password: ref(''),
    };
  },
  props: {
    buttonText: {
      type: String,
      default: 'Sign in',
    },
    registerForm: {
      type: Boolean,
      default: true,
    },
  },
  methods: {
    submitHandler(event: SubmitEvent | Event) {
      event.preventDefault();
      const data: TBody = {
        username: this.email,
        password: this.password,
      };
      const apiType: string = this.registerForm
        ? 'auth/register'
        : 'auth/login';
      api
        .post(apiType, data)
        .then((res) => {
          if (res.data) {
            this.$q.notify({
              message: 'Success',
              color: 'green',
              textColor: 'white',
            });
            if (!this.registerForm) {
              this.$q.localStorage.set('token', res.data.access_token);
              this.$router.push('/profile');
            }
          }
        })
        .catch((error: AxiosError) => {
          this.$q.notify({
            message: error.response?.data.message,
            color: 'red',
            textColor: 'white',
          });
        });
    },
  },
});
</script>

<style lang="scss">
.form {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
</style>
