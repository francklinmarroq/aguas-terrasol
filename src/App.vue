<template>
  <ul>
    <li v-for="instrument in instruments" :key="instrument.id">{{ instrument.name }}</li>
  </ul>
</template>
<script lang="ts" setup>
import { ref, onMounted } from "vue";
import { supabase } from "./lib/supabaseClient";

interface Instrument {
  id: number;
  name: string;
}

const instruments = ref<Instrument[]>([]);
async function getInstruments() {
  const { data } = await supabase.from("instruments").select();
  instruments.value = data ?? [];
}
onMounted(() => {
  getInstruments();
});
</script>
