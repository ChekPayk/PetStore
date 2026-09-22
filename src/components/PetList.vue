<template>
  <div>
    <div class="list-pets">
      <div v-for="item in petList?.filter((pet) => pet.name !== 'doggie')">
        <v-card :title="item.name" class="card" @click="openCard(item)" hover>
        </v-card>
      </div>
    </div>
    <v-dialog v-model="dialog" max-width="500">
      <v-card :title="selectedPet?.name">
        <v-card-text>
          <v-img
            v-if="selectedPet?.photoUrls?.[0] && !photoError"
            :src="selectedPet?.photoUrls?.[0]"
            height="200"
            contain
            @error="photoError = true"
            class="pet-photo"
          ></v-img>

          <div>Статус: {{ statusLabels[selectedPet?.status ?? ""] }}</div>
          <div>Категория: {{ selectedPet?.category?.name ?? "нет" }}</div>
        </v-card-text>
        <v-card-actions>
          <v-btn text="Закрыть" @click="dialog = false"></v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

    <!-- <v-list :items="doctorList" item-title="fio" variant="outlined"
    >

    </v-list> -->

    <!-- <v-autocomplete
      label="Врач"
      :items="doctorList" item-title="fio"
    >

    </v-autocomplete> -->
  </div>
</template>

<script lang="ts" setup>
// import {Pet} from "@/Api.ts"
import type { Pet } from "@/Api.ts";
import { Api } from "@/Api.ts";
import { onMounted, ref } from "vue";

interface Props {
  status: "available" | "pending" | "sold";
}

const statusLabels: Record<string, string> = {
  available: "Доступен",
  pending: "Забронирован",
  sold: "Нашел дом",
};

const props = defineProps<Props>();

const petApi = new Api();

const petList = ref<Array<Pet>>();

const dialog = ref(false);

const selectedPet = ref<Pet | null>(null);

const photoError = ref(false);

function openCard(petCard: Pet) {
  selectedPet.value = petCard;
  dialog.value = true;
  photoError.value = false;
}

onMounted(async () => {
  const response = await petApi.pet.findPetsByStatus({
    status: [props.status],
  });
  petList.value = response.data;
});
</script>

<style lang="scss" scoped>
.list-pets {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  gap: 10px;
}

.card {
  width: 140px;
  height: 150px;
}

.pet-photo :deep(img) {
  object-position: left;
}

</style>
