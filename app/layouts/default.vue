<template>
  <div>
    <!-- Simple header for landing page -->
    <header class="border-b border-default">
      <nav class="mx-auto flex max-w-7xl items-center justify-between p-6 lg:px-8">
        <div class="flex lg:flex-1">
          <NuxtLink to="/" class="-m-1.5 p-1.5">
            <span class="text-xl font-bold">Well Labs</span>
          </NuxtLink>
        </div>
        <div class="flex gap-x-4">
          <UColorModeButton />
          <UButton
            label="Dashboard"
            to="/dashboard"
            color="primary"
          />
        </div>
      </nav>
    </header>

    <UMain>
      <slot />
    </UMain>

    <!-- Simple footer for landing page -->
    <footer class="border-t border-default">
      <div class="mx-auto max-w-7xl px-6 py-12 lg:px-8">
        <p class="text-center text-sm text-muted">
          &copy; 2025 Well Labs. All rights reserved.
        </p>
      </div>
    </footer>
  </div>
</template>
