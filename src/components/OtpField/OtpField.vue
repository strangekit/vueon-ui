<script setup lang="ts">
import { ref, computed } from "vue"
import { PinInputRoot, PinInputInput } from "reka-ui"

/* ---------------- Props ---------------- */

const props = defineProps({
  length: {
    type: Number,
    default: 6,
  },
  variant: {
    type: String as () => "default" | "capsule" | "grouped",
    default: "default",
  },
})

/* ---------------- State ---------------- */

const otp = ref<string[]>(Array(props.length).fill(""))

/* ---------------- Complete Detection ---------------- */

const isComplete = computed(() =>
  otp.value.length === props.length &&
  otp.value.every((digit) => digit !== "")
)

/* ---------------- Group Logic (pairs of 2) ---------------- */

const groupedIndexes = computed(() => {
  if (props.variant !== "grouped") return []

  const groups = []
  for (let i = 0; i < props.length; i += 2) {
    groups.push([i, i + 1])
  }
  return groups
})
</script>

<template>
  <div class="flex w-full justify-center">

    <!-- ================= DEFAULT ================= -->

    <PinInputRoot
      v-if="variant === 'default'"
      v-model="otp"
      class="flex gap-2"
    >
      <PinInputInput
        v-for="index in length"
        :key="index"
        :index="index - 1"
        :class="[
          'w-10 h-10 text-center border rounded-md text-base font-medium transition-all outline-0',
          'focus-within:ring-2 focus-within:ring-ring/70',
          isComplete ? 'bg-secondary text-secondary-foreground' : 'bg-background'
        ]"
      />
    </PinInputRoot>

    <!-- ================= CAPSULE ================= -->

    <PinInputRoot
  v-else-if="variant === 'capsule'"
  v-model="otp"
  :class="[
    'flex overflow-hidden border rounded-full transition-all duration-200',
    'focus-within:ring-2 focus-within:ring-ring/70 ',
    isComplete ? 'bg-secondary' : 'bg-background'
  ]"
>
  <PinInputInput
    v-for="(index, i) in length"
    :key="index"
    :index="index - 1"
    :class="[
      'w-10 h-10 text-center bg-transparent outline-none ',
      i !== length - 1 ? 'border-r border-border/50' : ''
    ]"
  />
</PinInputRoot>
    <!-- ================= GROUPED ================= -->

    <PinInputRoot
  v-else
  v-model="otp"
  class="flex gap-4"
>
  <template v-for="(group, gIndex) in groupedIndexes" :key="gIndex">
    <div
      :class="[
        'flex overflow-hidden border rounded-full transition-all duration-200',
        'focus-within:ring-2 focus-within:ring-ring/70',
        isComplete ? 'bg-secondary' : 'bg-background'
      ]"
    >
      <PinInputInput
        v-for="(i, idx) in group"
        :key="i"
        :index="i"
        :class="[
          'w-8 h-10 text-center bg-transparent outline-none',
          idx !== group.length - 1 ? 'border-r border-border/50' : ''
        ]"
      />
    </div>
  </template>
</PinInputRoot>
  </div>
</template>