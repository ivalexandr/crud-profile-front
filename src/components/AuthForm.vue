<template>
  <q-form class="form">
    <q-input
      rounded
      outlined
      clearable
      type="email"
      v-model="email"
      label="Email"
      name="email"
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
    >
      <template v-slot:append>
        <q-icon name="password" />
      </template>
    </q-input>
    <q-btn type="submit" color="purple">
      {{ buttonText }}
    </q-btn>
  </q-form>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { ref } from 'vue';

export default defineComponent({
  name: 'AuthForm',
  setup() {
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
