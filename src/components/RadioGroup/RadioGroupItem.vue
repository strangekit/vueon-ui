<script setup lang="ts">
import { RadioGroupItem, RadioGroupIndicator } from "reka-ui"
import { defineProps } from "vue"

const props = defineProps<{
  id: string
  value: string
  class?: string
}>()
</script>

<template>
  
  <RadioGroupItem
  :id="props.id"
  :value="props.value"
  :class="[
    'group relative h-4 w-4 rounded-full border border-input text-primary',
    'flex items-center justify-center',
    'transition-all duration-200 ease-out',

    'active:scale-90',
    'data-[state=checked]:scale-105',


    'focus:outline-none focus-visible:ring-2 focus-visible:ring-ring/70 focus-visible:ring-offset-2',

    'ring-offset-background disabled:opacity-50 disabled:cursor-not-allowed',
    props.class
  ]"
>
  <div
    class="
      h-2.5 w-2.5 rounded-full bg-current
      scale-0
      transition-transform duration-200 ease-out
      group-data-[state=checked]:scale-100
    "
  ></div>
</RadioGroupItem>
</template>
