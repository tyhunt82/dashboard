<script setup lang="ts">
const route = useRoute()
const path = `/blog/${Array.isArray(route.params.slug) ? route.params.slug.join('/') : route.params.slug || ''}`
const { data: page } = await useAsyncData(`blog-${path}`, async () => {
  const posts = await queryCollection('posts').all()
  return posts.find(post => post._path === path)
})

if (!page.value) {
  throw createError({
    statusCode: 404,
    statusMessage: 'Page Not Found'
  })
}

const title = page.value?.title || 'Blog Post'
const description = page.value?.description || ''

useSeoMeta({
  titleTemplate: '%s • Blog',
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
      <UProse>
        <MDC :value="page" />
      </UProse>
    </UPageBody>
  </UPage>
</template>

