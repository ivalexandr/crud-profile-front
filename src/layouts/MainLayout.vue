<template>
  <q-layout view="lHh Lpr lFf">
    <q-toolbar class="bg-purple text-white">
      <q-toolbar-title> Crud-front </q-toolbar-title>
    </q-toolbar>
  </q-layout>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'MainLayout',

  setup() {
    const leftDrawerOpen = ref(false);

    return {
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
});
</script>
