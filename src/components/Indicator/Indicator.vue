<script setup lang="ts">
import { computed, useAttrs } from "vue"
import { variants } from "@/components/theme"

const $attrs = useAttrs()

const props = defineProps<{
  value?: string | number
  variant?: 
    | "default"
    | "destructive"
    | "outline"
    | "secondary"
    | "informative"
    | "positive"
    | "caution"
  size?: "sm" | "md" | "lg" | "icon"
  rounded?: boolean
  relativeMode?: boolean
  position?:
    | "top-left"
    | "top-right"
    | "top-center"
    | "bottom-left"
    | "bottom-right"
    | "bottom-center"
    | "center"
}>()

/* Absolute positioning map */
const positionClasses: Record<string, string> = {
  "top-left": "top-0 left-0 -translate-x-1/2 -translate-y-1/2",
  "top-right": "top-0 right-0 translate-x-1/2 -translate-y-1/2",
  "top-center": "top-0 left-1/2 -translate-x-1/2 -translate-y-1/2",
  "bottom-left": "bottom-0 left-0 -translate-x-1/2 translate-y-1/2",
  "bottom-right": "bottom-0 right-0 translate-x-1/2 translate-y-1/2",
  "bottom-center": "bottom-0 left-1/2 -translate-x-1/2 translate-y-1/2",
  center: "top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2",
}

/* Size styles */
const sizeMap: Record<string, string> = {
  sm: "h-6 w-6 text-[0.6rem] px-1",
  md: "h-7 w-7 text-xs px-1.5",
  lg: "h-9 w-9 text-sm px-2",
  icon: "h-5 w-5 text-[0.55rem]",
}

const sizeClasses = computed(() => sizeMap[props.size ?? "md"])
const roundedClass = computed(() =>
  props.rounded ? "rounded-full" : "rounded-md"
)

/* Let Vue normalize class properly (string | array | object) */
const attrsClass = computed(() => $attrs.class)

/* Wrapper & positioning */
const wrapperClass = computed(() =>
  props.relativeMode ? "relative inline-block" : "inline-block"
)

const indicatorPositionClass = computed(() =>
  props.relativeMode ? "absolute" : "inline-flex"
)

/* Display logic */
const hasValue = computed(() => props.value !== undefined && props.value !== null)
</script>

<template>
  <div :class="wrapperClass">
    <slot />

    <span
      v-if="hasValue || $slots.indicator"
      :class="[
        indicatorPositionClass,
        'flex items-center justify-center font-medium leading-none select-none pointer-events-none transition-all',
        sizeClasses,
        roundedClass,
        variants({ variant: props.variant ?? 'default' }),
        props.relativeMode
          ? positionClasses[props.position ?? 'top-right']
          : '',
        attrsClass
      ]"
    >
      <!-- If value prop exists -->
      <template v-if="hasValue">
        {{ props.value }}
      </template>

      <!-- Otherwise use named slot -->
      <slot v-else name="indicator" />
    </span>
  </div>
</template>