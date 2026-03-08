<script setup lang="ts">
import { ref, computed } from 'vue' // 1. Added imports
import Input from "@/components/ui/Input/Input.vue"
import registry from "../../../../registry.json"
import DocsNavigation from "../../components/DocsNavigation.vue"
import { SearchIcon } from "lucide-vue-next"

interface ComponentItem {
  path: string
  description: string
  status: string
}

const getStatusColor = (status: string) => {
  switch (status) {
    case "stable": return "bg-green-500"
    case "experimental": return "bg-blue-500"
    case "rookie": return "bg-yellow-500"
    default: return "bg-gray-300"
  }
}

// 2. State for the search query
const searchQuery = ref("")

// 3. Computed property to filter components
const filteredComponents = computed(() => {
  const entries = Object.entries(registry.components) as [string, ComponentItem][]
  
  if (!searchQuery.value) return entries

  const query = searchQuery.value.toLowerCase()
  
  return entries.filter(([name, item]) => 
    name.toLowerCase().includes(query) || 
    item.description.toLowerCase().includes(query)
  )
})
</script>

<template>
  <DocsNavigation
    :prev="{ title: 'Cli', path: '/docs/cli' }"
    :next="{ title: '', path: '' }"
  /> 
  
  <div class="">
    <h1 class="text-3xl font-bold mb-6">UI Components</h1>
    
    <div class="flex items-center gap-2 mb-6 relative">
      <div class="relative w-full ">
        <SearchIcon class="absolute right-3 top-1/2 -translate-y-1/2 h-4 w-4 text-muted-foreground" />
        <Input 
          v-model="searchQuery" 
          class="" 
          placeholder="Search Component Here..."
        />
      </div>
    </div>

    <div class="mt-1 grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
      <router-link
        v-for="[name, item] in filteredComponents"
        :key="name"
        :to="{ name: 'doc-components-list-items', params: { items: name } }"
        class="
        border 
        border-input 
        rounded-lg p-4 
        hover:border-primary/50 
        hover:shadow-md 
        transition-all 
        block 
        bg-card 
        text-card-foreground 
        focus-visible:border-ring 
        focus-visible:ring-ring/50 
        focus-visible:ring-[2px] 
        focus-visible:outline-none "
      >
        <div class="flex items-center justify-start gap-2 mb-1">
          <h2 class="font-semibold text-lg">{{ name }}</h2>
          <span
            title="Status"
            :class="[
              'w-2 h-2 rounded-full block',
              getStatusColor(item.status)
            ]"
          ></span>
        </div>
        <p class="text-sm text-muted-foreground line-clamp-2">{{ item.description }}</p>
      </router-link>

      <div v-if="filteredComponents.length === 0" class="col-span-full py-10 text-center text-muted-foreground">
        No components found matching "{{ searchQuery }}"
      </div>
    </div>
  </div>
</template>