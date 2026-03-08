<template>
  <div class="space-y-10 w-full max-w-4xl pb-20">
    <DocsNavigation
      :prev="{ title: 'Registry', path: '/docs/registry' }"
      :next="{ title: 'Blocks', path: '/docs/blocks' }"
    />

    <header class="space-y-2">
      <h1 class="text-4xl font-extrabold tracking-tight">Changelog</h1>
      <p class="text-lg text-muted-foreground leading-relaxed">
        Real-time updates and version history for the Vueon-UI ecosystem.
      </p>
    </header>

    <div class="flex flex-wrap gap-3 items-center p-1">
      <div class="relative flex-1 min-w-[240px]">
        <!-- <SearchIcon class="absolute left-3 top-1/2 -translate-y-1/2 h-4 w-4 text-muted-foreground" /> -->
        <Input
          v-model="search"
          placeholder="Filter updates..."
          class=" h-10 border-muted focus-visible:ring-primary/20"
        />
      </div>

      <div class="flex gap-2">
        <SelectRoot v-model="selectedYear">
          <SelectTrigger class="w-[120px] h-10 bg-card text-sm">
            {{ selectedYear === 'all' ? 'All Years' : selectedYear }}
          </SelectTrigger>
          <SelectContent>
            <SelectItem value="all">All Years</SelectItem>
            <SelectItem v-for="y in years" :key="y" :value="y">{{ y }}</SelectItem>
          </SelectContent>
        </SelectRoot>

        <SelectRoot v-model="selectedMonth">
          <SelectTrigger class="w-[130px] h-10 bg-card text-sm">
             {{ selectedMonth === 'all' ? 'All Months' : `Month: ${selectedMonth}` }}
          </SelectTrigger>
          <SelectContent>
            <SelectItem value="all">All Months</SelectItem>
            <SelectItem v-for="m in months" :key="m" :value="m">{{ m }}</SelectItem>
          </SelectContent>
        </SelectRoot>
      </div>
    </div>

    <div v-if="filteredItems.length" class="space-y-0 border-l border-muted ml-4 md:ml-6">
      <div
        v-for="item in filteredItems"
        :key="item.name"
        class="relative pl-8 pb-12 group transition-all"
      >
        <div class="absolute left-[-5px] top-1.5 w-2.5 h-2.5 bg-muted rounded-full border-2 border-background ring-4 ring-background group-hover:bg-primary group-hover:scale-125 transition-all duration-300"></div>

        <div class="flex items-center gap-2 mb-2">
          <CalendarIcon class="w-3.5 h-3.5 text-muted-foreground" />
          <time class="text-xs font-mono font-medium text-muted-foreground uppercase tracking-widest">
            {{ item.updated }}
          </time>
          <span v-if="isNew(item.updated)" class="text-[10px] bg-primary/10 text-primary px-2 py-0.5 rounded-full font-bold uppercase">New</span>
        </div>

        <div class="bg-card/40 border border-transparent group-hover:border-muted group-hover:bg-card p-5 rounded-xl transition-all shadow-sm group-hover:shadow-md">
          <div class="flex justify-between items-start gap-4">
            <div class="space-y-1">
              <h2 :id="item.name" class="text-xl font-bold tracking-tight">
                {{ item.name }}
              </h2>
              <p class="text-muted-foreground leading-relaxed">
                {{ item.description }}
              </p>
            </div>
            
            <RouterLink :to="`/docs/components/${item.name}`">
              <Button variant="outline" size="sm" class="h-8 gap-2 bg-background hover:bg-primary hover:text-white border-muted">
                Explore <ArrowRightIcon class="w-3.5 h-3.5" />
              </Button>
            </RouterLink>
          </div>
        </div>
      </div>
    </div>

    <div v-else class="flex flex-col items-center justify-center py-20 border-2 border-dashed rounded-3xl border-muted">
      <div class="p-4 bg-muted/50 rounded-full mb-4">
        <SearchIcon class="w-8 h-8 text-muted-foreground/50" />
      </div>
      <h3 class="text-lg font-medium">No matching updates</h3>
      <p class="text-muted-foreground">Try adjusting your filters or search term.</p>
      <Button variant="link" @click="resetFilters" class="mt-2">Clear all filters</Button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from "vue"
import registry from "../../../../registry.json"
import DocsNavigation from "../../components/DocsNavigation.vue"
import { Button } from "../../components/ui/Button"
import Input from "../../components/ui/Input"
import { SelectRoot, SelectTrigger, SelectContent, SelectItem } from "../../components/ui/Select"
import { SearchIcon, CalendarIcon, ArrowRightIcon } from "lucide-vue-next"

interface ChangeItem {
  description: string
  updated?: string
}

const rawItems = Object.entries(registry.components).map(([name, data]) => {
  const d = data as ChangeItem
  return {
    name,
    description: d.description,
    updated: d.updated ?? ""
  }
}).filter(i => i.updated.trim() !== "")

const normalize = (d: string) => {
  const [dd, mm, yyyy] = d.split("/")
  return `${yyyy}-${mm}-${dd}`
}

const items = rawItems.sort((a, b) => {
  return new Date(normalize(b.updated)).getTime() - new Date(normalize(a.updated)).getTime()
})

const months = [...new Set(items.map(i => i.updated.split("/")[1]))].sort()
const years = [...new Set(items.map(i => i.updated.split("/")[2]))].sort((a, b) => b.localeCompare(a))

const search = ref("")
const selectedMonth = ref("all")
const selectedYear = ref("all")

const resetFilters = () => {
  search.value = ""
  selectedMonth.value = "all"
  selectedYear.value = "all"
}

// Logic for "New" badge (e.g., updated in the last 30 days)
const isNew = (dateStr: string) => {
  const date = new Date(normalize(dateStr))
  const diff = new Date().getTime() - date.getTime()
  return diff < 1000 * 60 * 60 * 24 * 30 // 30 days
}

const filteredItems = computed(() => {
  return items.filter(item => {
    const [_dd, mm, yyyy] = item.updated.split("/")
    const matchSearch = item.name.toLowerCase().includes(search.value.toLowerCase()) ||
                        item.description.toLowerCase().includes(search.value.toLowerCase())
    const matchMonth = selectedMonth.value === "all" || selectedMonth.value === mm
    const matchYear = selectedYear.value === "all" || selectedYear.value === yyyy
    return matchSearch && matchMonth && matchYear
  })
})
</script>