<template>
  <q-form class="profile-form" @submit="submitHandler">
    <q-input
      rounded
      outlined
      type="text"
      v-model="name"
      label="name"
      name="name"
    />
    <q-input
      rounded
      outlined
      type="text"
      v-model="address"
      label="Address"
      name="address"
    />
    <q-input
      rounded
      outlined
      v-model="phone"
      label="Phone"
      name="phone"
      mask="(###) ### - ####"
      unmasked-value
      fill-mask
    />
    <q-input
      rounded
      outlined
      v-model="about"
      label="About yourself"
      type="textarea"
      name="about"
      autogrow
    />
    <q-btn rounded color="purple" type="submit">Save</q-btn>
  </q-form>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import { useQuasar } from 'quasar';
import { TResponseData } from './types';
import { api } from 'src/boot/axios';
import { AxiosError } from 'axios';

export default defineComponent({
  setup() {
    //eslint-disable-next-line
    const $q = useQuasar();
    return {
      name: ref(''),
      address: ref(''),
      phone: ref(''),
      about: ref(''),
    };
  },
  mounted() {
    if (!this.$q.localStorage.getItem('token')) {
      this.$router.push('/');
      return;
    }
    api
      .get('profile/user', {
        headers: {
          Authorization: `Bearer ${this.$q.localStorage.getItem('token')}`,
        },
      })
      .then((res) => {
        const { name, phone, about, address } = res.data;
        this.name = name;
        this.phone = phone;
        this.about = about;
        this.address = address;
      });
  },

  methods: {
    submitHandler(event: SubmitEvent | Event) {
      event.preventDefault();
      const data: TResponseData = {
        name: this.name,
        about: this.about,
        address: this.address,
        phone: this.phone,
      };
      api
        .patch('profile/user', data, {
          headers: {
            Authorization: `Bearer ${this.$q.localStorage.getItem('token')}`,
          },
        })
        .then((res) => {
          if (res.data) {
            this.$q.notify({
              message: 'Success',
              color: 'green',
              textColor: 'white',
            });
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
.profile-form {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
</style>
