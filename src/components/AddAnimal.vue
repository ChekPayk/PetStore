<template>
  <v-dialog max-width="500">
    <template v-slot:activator="{ props: activatorProps }">
      <v-btn
        icon="mdi-plus"
        v-bind="activatorProps"
        text="Open Dialog"
        variant="flat"
        size="small"
        color="#2196F3"
      ></v-btn>
    </template>

    <template v-slot:default="{ isActive }">
      <v-card title="Dialog">
        <v-card-text>
          Добавим писну
          <v-text-field></v-text-field>
        </v-card-text>

        <v-card-actions>
          <v-btn text="Закрыть" @click="isActive.value = false"></v-btn>
          <v-spacer></v-spacer>
          <v-btn text="Добавить" @click="onAddAnimal"></v-btn>
        </v-card-actions>
      </v-card>
    </template>
  </v-dialog>
</template>

<script lang="ts" setup>
import { Api } from "@/Api.ts";
const petApi = new Api();

async function onAddAnimal() {
  const response = await petApi.pet.addPet({
    id: 13,
    category: {
      id: 12,
      name: "cat",
    },
    name: "Kitty1",
    photoUrls: [],
    tags: [],
    status: "available",
  });
  console.log("trrrr");
}
</script>
