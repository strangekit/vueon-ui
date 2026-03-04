<script setup lang="ts">
import { CollapsibleContent as RekaContent } from "reka-ui"
import './style.css';
</script>

<template>
  <RekaContent
    class="CollapsibleContent text-sm text-muted-foreground "
  >
    <slot />
  </RekaContent>
</template>

<script lang="ts">
export default { name: "CollapsibleContent" }
</script>
