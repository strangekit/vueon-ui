<script setup lang="ts">
import { MenubarItem } from 'reka-ui'
</script>

<template>
  <MenubarItem
    v-bind="$attrs"
    class="relative flex cursor-default select-none items-center rounded-sm px-2 py-1.5 text-sm outline-none 
           focus:bg-accent focus:text-accent-foreground active:scale-[0.98] transition-transform duration-100"
  >
    <slot />
  </MenubarItem>
</template>
