<template>
  <div>
    <div class="list-pets">
      <div v-for="item in petList" class="card">
        <v-card :title="item.name">
          <v-card-actions>
            <v-btn>Click me</v-btn>
          </v-card-actions>
        </v-card>
      </div>
    </div>
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
const petApi = new Api();

const petList = ref<Array<Pet>>();

onMounted(async () => {
  // const pets:Pet = await (await petApi.pet.getPetById(10)).data

  petList.value = await (
    await petApi.pet.findPetsByStatus({ status: ["available"] })
  ).data;
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
  border: black;
}

</style>
