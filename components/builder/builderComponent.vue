<script setup>
import {REGISTERED_COMPONENTS} from "../../init-builder"
import {
  RenderContent,
  isPreviewing,
  fetchEntries,
  fetchOneEntry
} from "@builder.io/sdk-vue";

const {model} = defineProps({
  model: {
    type: String,
    default: "page",
  }
})

console.log(model)

const runtimeConfig = useRuntimeConfig();

const BUILDER_PUBLIC_API_KEY = runtimeConfig.public.BUILDER_KEY;

const route = useRoute();

// fetch builder content data
const content = await fetchOneEntry({
  model: model,
  apiKey: BUILDER_PUBLIC_API_KEY,
  userAttributes: {
    urlPath: route.path,
  },
  options: {enrich: true}
})
console.log(content)
</script>

<template>
  <Head>
    <Title>{{ content?.data?.title }}</Title>
    <Meta name="description" :content="content?.data?.description"/>
    <Meta v-if="content?.data?.addNoIndex" name="robots" content="nofollow"/>
  </Head>
  <div id="home">
    <div v-if="content || isPreviewing()">
      <RenderContent
          :model="model"
          :content="content"
          :api-key="BUILDER_PUBLIC_API_KEY"
      />
    </div>
    <div v-else>Content not Found</div>
  </div>
</template>
