<template>
  <div id="home">
    <div v-if="content || isPreviewing()">
      <RenderContent
        model="surinder-2"
        :content="content"
        :api-key="BUILDER_PUBLIC_API_KEY"
      />
    </div>
    <div v-else>Content not Found</div>
  </div>
</template>

<script setup>
import {
  RenderContent,
  fetchOneEntry,
  isPreviewing,
} from "@builder.io/sdk-vue";

const BUILDER_PUBLIC_API_KEY = "fdc38f2e8eee4fcc90e72279fdb8708c";

const route = useRoute();

// fetch builder content data
const content = await fetchOneEntry({
  model: "surinder-2",
  apiKey: BUILDER_PUBLIC_API_KEY,
  userAttributes: {
    urlPath: route.path,
  },
});
console.log(content);
</script>
