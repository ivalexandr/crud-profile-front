<template>
  <q-page class="row items-center justify-evenly">
    <div class="profile-form-wrapper">
      <h3 class="profile-header">Profile</h3>
      <ProfileForm />
    </div>
  </q-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import ProfileForm from 'src/components/ProfileForm/ProfileForm.vue';

export default defineComponent({
  name: 'ProfilePage',
  components: { ProfileForm },
});
</script>

<style lang="scss">
.profile-form-wrapper {
  width: 400px;
}
.profile-header {
  padding: 0;
  margin: 0;
  margin-bottom: 15px;
}
</style>
