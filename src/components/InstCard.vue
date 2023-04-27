<template>
  <v-card v-if="searched" style="position: relative" class="">
    <v-card-title
      style="white-space: unset"
      v-html="inst.names.join('<br/>')"
    />
    <v-card-subtitle v-if="inst.locations.length" style="white-space: unset">
      <b>地址：</b>
      <template v-for="(loc, idx) in inst.locations" :key="idx">
        <p v-if="!idx || expandAddress">{{ loc }}</p>
      </template>
      <v-chip
        @click="expandAddress = !expandAddress"
        v-if="inst.locations.length > 1"
        size="x-small"
        :text="
          expandAddress ? '收回' : '展开' + `(+${inst.locations.length - 1})`
        "
      ></v-chip>
    </v-card-subtitle>
    <v-card-subtitle v-if="inst.sites.length" style="white-space: unset">
      <b>网站：</b>
      <template v-for="(loc, idx) in inst.sites" :key="idx">
        <p v-if="!idx || expandAddress">{{ loc }}</p>
      </template>
      <v-chip
        @click="expandAddress = !expandAddress"
        v-if="inst.sites.length > 1"
        size="x-small"
        :text="expandAddress ? '收回' : '展开' + `(+${inst.sites.length - 1})`"
      ></v-chip>
    </v-card-subtitle>
    <v-divider class="mt-2" />
    <v-card-actions>
      <SourceList :inst="inst" />
      <v-spacer />
      <EvidenceList :inst="inst" />
      <v-chip class="mx-1" label :color="inst.checked ? 'error' : 'grey'">{{
        inst.checked ? "已审核" : "待审核"
      }}</v-chip>
    </v-card-actions>
  </v-card>
</template>

<script setup>
import SourceList from "./SourceList.vue";
import EvidenceList from "./EvidenceList.vue";
import { ref } from "vue";
const { inst, searched } = defineProps(["inst", "searched"]);
const expandAddress = ref(false);
const expandLink = ref(false);
</script>
