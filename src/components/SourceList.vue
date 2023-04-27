<template>
  <v-chip class="mx-1" label @click="openDialog" color="grey">{{
    labelStr(inst)
  }}</v-chip>
  <v-dialog v-model="dialog" width="auto">
    <v-card max-width="500px" min-width="300px">
      <v-list>
        <v-list-item
          prepend-icon="mdi-alert"
          v-for="e in inst.sources"
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
  dialog.value = true;
};
const labelStr = (it) => {
  return `${it.sources.length} 条来源`;
};
</script>
