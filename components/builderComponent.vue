<template>
  <div id="home">
    <div v-if="content || isPreviewing()">
      <Content
          :model="model"
          :content="content"
          :api-key="BUILDER_PUBLIC_API_KEY"
          :data="user_data"
      />
    </div>
    <div v-else>Content not Found</div>
  </div>
</template>

<script setup>
import {Content, fetchOneEntry, isPreviewing} from "@builder.io/sdk-vue";

const {model, user_data} = defineProps({
  model: {
    type: String,
    default: "surinder",
    require: true,
  },
  user_data: {
    type: Object,
    require: true,
  },
});

const content = ref(null);
const BUILDER_PUBLIC_API_KEY = "fdc38f2e8eee4fcc90e72279fdb8708c";
const route = useRoute();

watchEffect(async () => {
  const res = await fetchOneEntry({
    model: model,
    apiKey: BUILDER_PUBLIC_API_KEY,
    userAttributes: {
      urlPath: route.path,
      ...user_data,
    },
  });
  content.value = res;
});
</script>

<style scoped></style>

<!--<template>-->
<!--  <div id="home">-->
<!--    <div v-if="content || isPreviewing()">-->
<!--      <button class="age-toggle-btn" @click="toggleAgeGroup()">Click to toggle Age Group</button>-->
<!--      <RenderContent-->
<!--          model="surinder-2"-->
<!--          :content="content"-->
<!--          :api-key="BUILDER_PUBLIC_API_KEY"-->
<!--          :data='{agegroup: agegroup}'-->
<!--      />-->
<!--    </div>-->
<!--    <div v-else>Loading Content...</div>-->
<!--  </div>-->
<!--</template>-->

<!--<script setup>-->
<!--import {-->
<!--  RenderContent,-->
<!--  fetchOneEntry,-->
<!--  isPreviewing,-->
<!--} from "@builder.io/sdk-vue";-->

<!--const agegroup = ref("default");-->
<!--const content = ref(null);-->

<!--const BUILDER_PUBLIC_API_KEY = "fdc38f2e8eee4fcc90e72279fdb8708c";-->
<!--const route = useRoute();-->

<!--watchEffect(async () => {-->
<!--// fetch builder content data-->
<!--  const data = await fetchOneEntry({-->
<!--    model: "surinder-2",-->
<!--    apiKey: BUILDER_PUBLIC_API_KEY,-->
<!--    userAttributes: {-->
<!--      urlPath: route.path,-->
<!--      agegroup: agegroup.value,-->
<!--    },-->
<!--  });-->
<!--  content.value = data;-->
<!--});-->

<!--const toggleAgeGroup = () => {-->
<!--  agegroup.value = agegroup.value === "child" ? "adult" : "child";-->
<!--}-->

<!--</script>-->

<!--<style scoped>-->
<!--.age-toggle-btn {-->
<!--  background-color: #4CAF50;-->
<!--  border: none;-->
<!--  color: white;-->
<!--  padding: 15px 32px;-->
<!--  text-align: center;-->
<!--  text-decoration: none;-->
<!--  display: inline-block;-->
<!--  font-size: 16px;-->
<!--  position: absolute;-->
<!--  top: 0;-->
<!--  right: 0;-->
<!--  z-index: 9999;-->
<!--}-->
<!--</style>-->
