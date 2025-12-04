<script setup lang="ts">
definePageMeta({
  layout: 'landing'
})

const { data: page } = await useAsyncData('pricing', () => queryCollection('pricing').first())

const title = page.value?.seo?.title || page.value?.title || 'Pricing'
const description = page.value?.seo?.description || page.value?.description || ''

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
      <UPageSection>
        <UPageGrid>
          <UPageCard
            v-for="(plan, index) in page.plans"
            :key="index"
            v-bind="plan"
            :highlight="plan.highlight"
          />
        </UPageGrid>
      </UPageSection>

      <UPageSection
        v-if="page.logos"
        :title="page.logos.title"
      >
        <UPageColumns class="xl:columns-5">
          <UIcon
            v-for="(icon, index) in page.logos.icons"
            :key="index"
            :name="icon"
            class="size-12 text-muted"
          />
        </UPageColumns>
      </UPageSection>

      <UPageSection
        v-if="page.faq"
        :title="page.faq.title"
        :description="page.faq.description"
      >
        <UPageAccordion :items="page.faq.items" />
      </UPageSection>
    </UPageBody>
  </UPage>
</template>

