<template>
  <v-chip
    class="mx-1"
    label
    @click="openDialog"
    :color="inst.persecution.known ? 'info' : 'grey'"
    >{{ labelStr(inst) }}</v-chip
  >
  <v-dialog v-model="dialog" width="auto">
    <v-card max-width="500px">
      <v-list>
        <v-list-item
          :href="e"
          prepend-icon="mdi-link"
          append-icon="mdi-arrow-right"
          v-for="e in inst.persecution.evidences"
          :key="e"
          >{{ e }}</v-list-item
        >
      </v-list>
    </v-card>
  </v-dialog>
</template>

<script setup>
import { ref } from "vue";
const { inst } = defineProps(["inst"]);
const dialog = ref(false);
const openDialog = () => {
  if (inst.persecution.evidences.length) dialog.value = true;
};
const labelStr = (it) => {
  if (!it.persecution.known) return "状况未知";
  if (!it.persecution.evidences.length) return "存在迫害";
  return `存在迫害，${it.persecution.evidences.length} 条证据`;
};
</script>
