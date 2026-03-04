<script setup lang="ts">
import { CheckboxRoot, CheckboxIndicator } from 'reka-ui'
import { Check } from 'lucide-vue-next'

defineProps({
  class: {
    type: String,
    default: ''
  }
})
</script>

<template>
  <CheckboxRoot
    :class="[
      'grid place-content-center peer h-4.5 w-4.5 shrink-0 rounded-sm border border-muted bg-muted ring-offset-background',
      'focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2',
      'disabled:cursor-not-allowed disabled:opacity-50',
      'data-[state=checked]:bg-primary data-[state=checked]:text-primary-foreground transition-colors',
      'transition-colors transition-transform duration-100 ease-out active:scale-[0.95]',
      $props.class
    ]"
  >
    <CheckboxIndicator class="grid place-content-center text-current">
      <Check class="h-4 w-4 p-0.5" />
    </CheckboxIndicator>
  </CheckboxRoot>
</template>
