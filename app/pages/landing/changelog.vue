<script setup lang="ts">
definePageMeta({
  layout: 'landing'
})

const { data: page } = await useAsyncData('changelog', () => queryCollection('changelog').first())
const { data: versions } = await useAsyncData('versions', () => queryCollection('versions').all())

const title = page.value?.title || 'Changelog'
const description = page.value?.description || ''

useSeoMeta({
  titleTemplate: '%s',
  title,
  ogTitle: title,
  description,
  ogDescription: description
})
</script>

<template>
  <UPage v-if="page">
    <UPageHeader
      :title="page.title"
      :description="page.description"
    />

    <UPageBody>
      <UPageTimeline>
        <UPageCard
          v-for="version in versions"
          :key="version._path"
          v-bind="version"
          :to="version._path"
        />
      </UPageTimeline>
    </UPageBody>
  </UPage>
</template>

