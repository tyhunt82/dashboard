<script setup lang="ts">
const route = useRoute()
const path = `/docs/${Array.isArray(route.params.slug) ? route.params.slug.join('/') : route.params.slug || ''}`
const { data: page } = await useAsyncData(`docs-${path}`, async () => {
  const docs = await queryCollection('docs').all()
  return docs.find(doc => doc._path === path)
})

if (!page.value) {
  throw createError({
    statusCode: 404,
    statusMessage: 'Page Not Found'
  })
}

const title = page.value?.seo?.title || page.value?.title || 'Docs'
const description = page.value?.seo?.description || page.value?.description || ''

useSeoMeta({
  titleTemplate: '%s • Docs',
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

