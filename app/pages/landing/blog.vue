<script setup lang="ts">
definePageMeta({
  layout: 'landing'
})

const { data: page } = await useAsyncData('blog', () => queryCollection('blog').first())
const { data: posts } = await useAsyncData('posts', () => queryCollection('posts').all())

const title = page.value?.title || 'Blog'
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
      <UPageGrid>
        <UPageCard
          v-for="post in posts"
          :key="post._path"
          v-bind="post"
          :to="post._path"
        />
      </UPageGrid>
    </UPageBody>
  </UPage>
</template>

