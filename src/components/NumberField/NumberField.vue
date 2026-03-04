<script setup lang="ts">
import { computed } from 'vue'
import { Minus, Plus } from 'lucide-vue-next'
import {
  NumberFieldRoot,
  NumberFieldInput,
  NumberFieldDecrement,
  NumberFieldIncrement
} from 'reka-ui'
import Label from '../Label/Label.vue'

/* ---------------- Props ---------------- */

const props = defineProps({
  label: {
    type: String,
    default: null
  },
  id: {
    type: String,
    default: ""
  },
  defaultValue: {
    type: Number,
    default: 18
  },
  min: {
    type: Number,
    default: 0
  },
  layout: {
    type: String as () => 'left' | 'center' | 'right',
    default: 'center'
  }
})

/* ---------------- Generated ID ---------------- */

const generatedId = computed(() => {
  if (props.id) return props.id
  if (props.label) return props.label.toLowerCase().replace(/\s+/g, "-")
  return "number-field"
})

/* ---------------- Layout Order ---------------- */

const layoutMap = computed(() => {
  return {
    left: ['input', 'decrement', 'increment'],
    center: ['decrement', 'input', 'increment'],
    right: ['increment', 'decrement', 'input']
  }[props.layout]
})
</script>

<template>
  <div class="flex flex-col gap-2 w-fit">
    
    <!-- Label -->
    <Label
      v-if="props.label"
      :for="generatedId"
      class="text-sm font-medium text-stone-700 dark:text-white"
    >
      {{ props.label }}
    </Label>

    <!-- Root -->
    <NumberFieldRoot
      :id="generatedId"
      :min="props.min"
      :default-value="props.defaultValue"
      class="flex items-center h-10 rounded-lg border border-border bg-card shadow-sm px-0.5 py-0.5 transition-colors duration-200 "
    >

      <template v-for="item in layoutMap" :key="item">

        <!-- INPUT -->
        <NumberFieldInput
          v-if="item === 'input'"
          class="h-full w-12 text-center focus:outline-none focus:ring-2 focus:ring-ring focus:ring-offset-1 transition-all duration-150 rounded-md"
        />

        <!-- DECREMENT -->
        <NumberFieldDecrement
          v-else-if="item === 'decrement'"
          class="h-full w-8 flex items-center justify-center rounded active:scale-[0.94] transition-transform duration-75 ease-out"
        >
          <Minus class="h-4 w-4" />
        </NumberFieldDecrement>

        <!-- INCREMENT -->
        <NumberFieldIncrement
          v-else
          class="h-full w-8 flex items-center justify-center rounded  active:scale-[0.94] transition-transform duration-75 ease-out"
        >
          <Plus class="h-4 w-4" />
        </NumberFieldIncrement>

      </template>

    </NumberFieldRoot>
  </div>
</template>