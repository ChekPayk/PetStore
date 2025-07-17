<template>
  <div>
    <!-- Врачи: {{ doctorList }} -->
    <li v-for="doctor in doctorList">
        {{ doctor.fio }}
    </li>

    <v-list :items="doctorList" item-title="fio" variant="outlined"
    >

    </v-list>

    <v-autocomplete
      label="Врач"
      :items="doctorList" item-title="fio"
    >

    </v-autocomplete>
  </div>

</template>

<script lang="ts" setup>

  interface Ticket {

  }

  interface Doctor {
    fio: string,
    specialization: string,
    room: string | number,
  }

  const doctorList:Array<Doctor> = [
    {
      fio: "Космодемьянская Лида Сергеевна",
      specialization: "врач-терапевт",
      room: "316 каб."
    },
    {
      fio: "Остапенко Борис Николаевич",
      specialization: "врач-стоматолог",
      room: "216 каб."
    },
    {
      fio: "Батицкая Вера Сергеевна",
      specialization: "врач-хирург",
      room: "317 каб."
    }
  ]

</script>
