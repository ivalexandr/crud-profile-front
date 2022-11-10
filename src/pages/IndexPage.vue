<template>
  <q-page class="row items-center justify-evenly">
    <div class="form-wrapper">
      <q-card>
        <q-tabs
          v-model="tab"
          dense
          class="text-grey"
          active-color="primary"
          indicator-color="primary"
          align="justify"
          narrow-indicator
        >
          <q-tab name="register" label="Sign up" />
          <q-tab name="login" label="Sign in" />
        </q-tabs>
        <q-separator />
        <q-tab-panels v-model="tab" animated>
          <q-tab-panel name="register">
            <AuthForm button-text="sign up" />
          </q-tab-panel>
          <q-tab-panel name="login">
            <AuthForm />
          </q-tab-panel>
        </q-tab-panels>
      </q-card>
    </div>
  </q-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { ref } from 'vue';
import AuthForm from '../components/AuthForm.vue';

export default defineComponent({
  name: 'IndexPage',
  components: { AuthForm },
  setup() {
    return {
      tab: ref('register'),
    };
  },
});
</script>

<style lang="scss">
.form-wrapper {
  width: 350px;
}
</style>
