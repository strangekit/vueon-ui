<script setup>
import { StepperTrigger as RekaStepperTrigger } from "reka-ui";
</script>

<template>
  <RekaStepperTrigger
    v-bind="$attrs"
    class="
     w-10 h-10 
          rounded-full 
          border 
          flex items-center justify-center 
          font-medium 
          transition-all
          data-[state=active]:bg-primary 
          data-[state=active]:text-primary-foreground
          data-[state=active]:border-border/50
          focus-within:ring-2 focus-within:ring-ring/70
           active:scale-[0.94] duration-75 ease-out
          data-[state=completed]:bg-primary
          data-[state=completed]:text-primary-foreground
          data-[state=completed]:border-primary
          data-[state=inactive]:bg-muted 
          data-[state=inactive]:text-muted-foreground 
          data-[state=inactive]:border-border/50
          mr-1
"
  >
    <slot />
  </RekaStepperTrigger>
</template>


<!-- cmd: git remote add  https://github.com/strangekit/vueon-ui.git -->