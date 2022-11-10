<template>
  <q-page class="column items-center justify-center">
    <div class="profile-logout">
      <q-btn @click="logoutHandler" type="button" color="grey" icon="logout"
        >Logout</q-btn
      >
    </div>
    <div class="profile-form-wrapper">
      <h3 class="profile-header">Profile</h3>
      <ProfileForm />
    </div>
  </q-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { useQuasar } from 'quasar';
import ProfileForm from 'src/components/ProfileForm/ProfileForm.vue';

export default defineComponent({
  name: 'ProfilePage',
  components: { ProfileForm },
  setup() {
    //eslint-disable-next-line
    const $q = useQuasar();
  },
  methods: {
    logoutHandler() {
      this.$q.localStorage.remove('token');
      this.$q.localStorage.remove('user');
      this.$router.push('/');
    },
  },
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
  font-size: 20px;
}
</style>
