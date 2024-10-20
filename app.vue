<template>
  <div class="px-14 py-12 text-white max-h-screen">
    <div class="grid grid-cols-2 gap-8 w-full ">
      <!-- Nilai Ujian Pekanan Section -->
      <div>
        <div class="text-2xl font-bold py-3">Nilai Ujian Pekanan</div>
        <div class="grid grid-cols-3 gap-4">
          <div v-for="i in 10" :key="i">
            <span>Pekan {{ i }}</span>
            <input class="input input-bordered" placeholder="Input value" v-model="data[`nilai_p${i}`]" type="number" />
          </div>
        </div>

        <!-- Nilai Di Kelas Section -->
        <div class="text-2xl font-bold py-3">Nilai Di Kelas</div>
        <div class="grid grid-cols-3 gap-4">
          <div v-for="(label, key) in kelasInputs" :key="key" class="grid">
            <span>{{ label }}</span>
            <input class="input input-bordered" placeholder="Input value" v-model="data[key]" type="number" />
          </div>
        </div>

        <div class="text-2xl font-bold py-3">Nilai Ujian Semester</div>
        <div class="grid grid-cols-3 gap-4">
          <div v-for="(label, key) in usInputs" :key="key" class="grid">
            <span>{{ label }}</span>
            <input class="input input-bordered" placeholder="Input value" v-model="data[key]" type="number" />
          </div>
        </div>

      </div>

      <!-- Result Section -->
      <div class="bg-slate-600 rounded-full h-[670px] grid place-items-center">
        <div class="w-full h-full flex flex-col justify-center items-center pb-[60px]">
          <p class="text-[260px] font-bold pb-3">{{ sum_nilai_up() }}</p>
          <p class="text5xl font-bold absolute bottom-[280px]">Nilai Rata-Rata</p>
        </div>
      </div>
    </div>
  </div>
  <div class="absolute bottom-0 left-3 text-[17px] font-semibold opacity-40">
    <p>@colonelwinchsell</p>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// Initializing all data properties dynamically
const data = ref({
  nilai_p1: 0, nilai_p2: 0, nilai_p3: 0, nilai_p4: 0, nilai_p5: 0, nilai_p6: 0, nilai_p7: 0, nilai_p8: 0, nilai_p9: 0, nilai_p10: 0,
  nilai_adab: 0, nilai_kehadiran: 0, nilai_us: 0
})

// Input labels for class-related values
const kelasInputs = {
  nilai_adab: 'Nilai Adab',
  nilai_kehadiran: 'Nilai kehadiran',
  // nilai_us: 'Nilai   US'
}

const usInputs = {
  nilai_us: 'Nilai US'
}

// Simplified sum function
const sum_nilai_up = () => {
  const total_up = [...Array(7)].reduce((sum, _, i) => sum + data.value[`nilai_p${i + 1}`], 0)
  const total_adab_akhlak = data.value.nilai_adab + data.value.nilai_kehadiran // 0.1
  const nilai_us = data.value.nilai_us

  return Math.floor((total_up / 10) * 0.2 + total_adab_akhlak + nilai_us * 0.6)
}

</script>
