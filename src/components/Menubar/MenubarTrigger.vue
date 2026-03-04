<script setup lang="ts">
import { MenubarTrigger } from 'reka-ui'
</script>

<template>
  <MenubarTrigger
    v-bind="$attrs"
    class="px-3 py-1.5 text-sm font-medium rounded-md hover:bg-accent hover:text-accent-foreground focus:outline-none focus:bg-accent focus:text-accent-foreground active:scale-[0.98] transition-transform duration-100"
  >
    <slot />
  </MenubarTrigger>
</template>
