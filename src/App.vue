<template>
  <v-app>
    <v-main>
      <v-container>
        <v-card class="text-center mb-2 pa-4">
          <v-card-title>
            <h2>未命名清单 | Unknown List</h2>
          </v-card-title>
          <v-card-subtitle style="white-space: unset">
            这是一份黑名单，来自 Trans Defense
            Project，列出了已确认和未确认的部分涉及非法进行跨性别扭转的机构及相关信息。
          </v-card-subtitle>
          <v-card-actions class="justify-center mt-4">
            <v-btn
              variant="outlined"
              href="https://github.com/FunctionSir/TransDefenseProject"
            >
              <v-icon start>mdi-github</v-icon>
              数据来源
            </v-btn>
          </v-card-actions>
        </v-card>
        <v-autocomplete
          v-model:model-value="searchVal"
          :loading="loading"
          class="mb-2"
          variant="solo"
          item-title="title"
          item-value="idx"
          hide-details
          closable-chips
          chips
          multiple
          label="搜索关键词"
          :items="searchData"
          @update:model-value="scrollData"
        ></v-autocomplete>
        <v-card
          v-if="loading"
          class="text-center"
          variant="tonal"
          text="加载中，稍安勿躁..."
        />
        <div class="card-container" v-if="!loading">
          <InstCard
            v-for="(inst, idx) in data"
            :key="idx"
            :inst="inst"
            :searched="searchVal.length == 0 || searchVal.includes(idx)"
          />
          <v-card class="text-center" :text="`2023 &copy; Everyone`" />
        </div>
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
import { ref } from "vue";
import InstCard from "./components/InstCard.vue";
const searchVal = ref([]);
const searchData = ref([]);
const data = ref([]);
const loading = ref(true);
const fetchData = () => {
  fetch(
    "https://raw.githubusercontent.com/FunctionSir/TransDefenseProject/master/institute_list.json"
  )
    .then((res) => res.json())
    .then((j) => {
      data.value = j["content"];
      for (let i = 0; i < j.length; i++) {
        searchData.value.push({
          title: j[i].names.join(","),
          idx: i,
        });
      }
      loading.value = false;
    });
};
const scrollData = () => {};
fetchData();
</script>

<style>
.card-container {
  column-count: 4;
}

@media only screen and (max-width: 720px) {
  .card-container {
    column-count: 1;
  }
}

@media only screen and (max-width: 1280px) and (min-width: 720px) {
  .card-container {
    column-count: 2;
  }
}

@media only screen and (max-width: 1820px) and (min-width: 1280px) {
  .card-container {
    column-count: 3;
  }
}

.card-container .v-card {
  display: inline-block;
  width: 100%;
}
</style>
