<template>
  <q-page class="row items-center justify-evenly">
    <div class="form-wrapper">
      <AuthForm />
    </div>
  </q-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import AuthForm from '../components/AuthForm.vue';

export default defineComponent({
  name: 'IndexPage',
  components: { AuthForm },
});
</script>

<style lang="scss">
.form-wrapper {
  width: 350px;
}
</style>
