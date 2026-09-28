<template>
  <v-app>
    <v-main>
      <v-app-bar :elevation="2" rounded>
        <template v-slot:prepend>
          <v-app-bar-nav-icon :icon="Logo"></v-app-bar-nav-icon>
        </template>

        <v-app-bar-title class="app-title">PetStore</v-app-bar-title>
        <div class="search-container">
          <v-text-field
            class="search-field"
            density="compact"
            hide-details
            variant="plain"
            v-model="searchDraft"
            append-inner-icon="mdi-magnify"
            @click:append-inner="getSearch()"
            @keyup.enter="getSearch()"
          />
        </div>
        <v-btn to="/" class="button" active-class="active-btn">
          Ищут дом
        </v-btn>
        <v-btn to="sold" class="button" active-class="active-btn">
          Выпускники
        </v-btn>
        <v-app-bar-actions>
          <AddAnimal />
        </v-app-bar-actions>
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
import AddAnimal from "@/components/AddAnimal.vue";
import { searchQuery } from "./composables/useSearch";
import { ref } from "vue";
const icons = [Vk, Telegram, Whatsapp];

const searchDraft = ref("");

function getSearch() {
  searchQuery.value = searchDraft.value;
}
</script>

<style lang="scss" scoped>
.app-title {
  flex: none;
  margin-right: 12px;
}

.app-footer {
  flex: none;
}

.button {
  text-transform: capitalize;
}

// .button:deep(.v-btn:active) {
//   background-color: aqua !important;;
// }

.active-btn {
  background-color: aqua !important;
}

.search-container {
  display: flex;
  flex-grow: 1;
  justify-content: start;
}

.search-field {
  max-width: 400px;
  width: 100%;
  padding: 8px 0;
  border: none;
  outline: none;
  font-size: 16px;
  background: transparent;
}
</style>
