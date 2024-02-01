<template>
  <div id="home">
    <div>Hello world from your Vue project. Below is Builder Content:</div>
    <div v-if="content || isPreviewing()">
      <div>
        page title:
        {{ content?.data?.title || 'Unpublished' }}
      </div>
      <RenderContent
          model="page"
          :content="content"
          :api-key="BUILDER_PUBLIC_API_KEY"
          :customComponents="REGISTERED_COMPONENTS"
      />
    </div>
    <div v-else>Content not Found</div>
  </div>
</template>

<script setup>
import {RenderContent, getContent, isPreviewing} from '@builder.io/sdk-vue';

const BUILDER_PUBLIC_API_KEY = 'fdc38f2e8eee4fcc90e72279fdb8708c';

const route = useRoute();

// fetch builder content data
const {data: content} = await useAsyncData('builderData', () =>
    getContent({
      model: 'surinder',
      apiKey: BUILDER_PUBLIC_API_KEY,
      userAttributes: {
        urlPath: route.path,
      },
    })
);
</script>