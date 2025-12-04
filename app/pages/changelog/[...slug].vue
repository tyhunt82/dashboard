<script setup lang="ts">
const route = useRoute()
const path = `/changelog/${Array.isArray(route.params.slug) ? route.params.slug.join('/') : route.params.slug || ''}`
const { data: page } = await useAsyncData(`changelog-${path}`, async () => {
  const versions = await queryCollection('versions').all()
  return versions.find(version => version._path === path)
})

if (!page.value) {
  throw createError({
    statusCode: 404,
    statusMessage: 'Page Not Found'
  })
}

const title = page.value?.title || 'Changelog Entry'
const description = page.value?.description || ''

useSeoMeta({
  titleTemplate: '%s • Changelog',
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

