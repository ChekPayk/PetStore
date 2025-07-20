<template>
  <v-app>
    <v-main>
      <v-app-bar :elevation="2" rounded>
        <template v-slot:prepend>
          <v-app-bar-nav-icon :icon="Logo"></v-app-bar-nav-icon>
        </template>

        <v-app-bar-title>PetStore</v-app-bar-title>
      </v-app-bar>
      <router-view />
    </v-main>
    <v-footer class="d-flex flex-column app-footer" color="blue" rounded="lg">
      <div class="d-flex w-100 align-center px-4 py-2">
        <strong>Свяжись с нами в социальных сетях!</strong>

        <div class="d-flex ga-2 ms-auto">
          <v-btn
            v-for="icon in icons"
            :key="icon"
            :icon="icon"
            size="small"
            variant="plain"
          ></v-btn>
        </div>
      </div>

      <div class="px-4 py-2 bg-surface-variant text-center w-100 rounded-lg">
        {{ new Date().getFullYear() }} — <strong>PetStore</strong>
      </div>
    </v-footer>
  </v-app>
</template>

<script lang="ts" setup>
import Logo from "@/components/icons/Logo.vue";
import Vk from "@/components/icons/Vk.vue";
import Telegram from "@/components/icons/Telegram.vue";
import Whatsapp from "@/components/icons/Whatsapp.vue";
const icons = [Vk, Telegram, Whatsapp];
</script>

<style lang="css" scoped>
.app-footer {
  flex: none;
}
</style>
