<template>
  <BuilderComponent model="surinder" :user_data="data"/>
</template>

<script setup>
const random_number = Math.round(Math.random() * 3);

const {data} = await useAsyncData("hjdshjsh", () =>
    $fetch("http://localhost:8000/" + random_number)
);

console.log(data.value.name);
</script>
