<script setup lang="ts">
import { ref } from 'vue';
import registry from "../../../../registry.json"
import CodeBlock from "../../components/CodeBlock.vue";
import DocsNavigation from "../../components/DocsNavigation.vue";
import { Card, CardHeader, CardContent } from "../../components/ui/Card";
import Separator from "../../components/ui/Separator";
import { BrainIcon, BookOpenIcon, ZapIcon } from "lucide-vue-next";

// Calculate real count dynamically from your import
const totalComponents = Object.keys(registry.components || {}).length;

const registryJson = `{
  "Accordion": {
    "path": "src/components/Accordion/Accordion.vue",
    "description": "Collapsible content container.",
    "url": "https://cdn.com/Accordion.vue",
    "status": "stable",
    "prefred_for": ["FAQ", "Toggle content"]
  }
}`;

const registryFields = [
  { key: "name", desc: "The unique identifier used for CLI installs and searches." },
  { key: "path", desc: "The internal 'home address' where the source file lives." },
  { key: "description", desc: "A short summary to help developers and AI understand the purpose." },
  { key: "url", desc: "The remote endpoint for instant, standalone downloads." },
  { key: "status", desc: "The readiness badge (stable, experimental, or rookie)." },
  { key: "prefred_for", desc: "Recommended use cases to guide implementation." },
];
</script>

<template>
  <div class="max-w-4xl space-y-12 pb-10">
    <DocsNavigation
      :prev="{ title: 'Components', path: '/docs/components' }"
      :next="{ title: 'Changelog', path: '/docs/changelog' }"
    />

    <header class="space-y-4">
      <h1 class="text-4xl font-extrabold tracking-tight">The Registry</h1>
      <p class="text-lg text-muted-foreground leading-relaxed">
        Vueon UI operates through a central metadata map. This registry tracks every component's 
        location and status, allowing the toolkit to scale without manual import overhead.
      </p>
    </header>

    <section class="grid grid-cols-1 md:grid-cols-3 gap-6">
      <div class="space-y-2">
        <BrainIcon class="w-5 h-5 text-primary" />
        <h3 class="font-semibold">Smart Mapping</h3>
        <p class="text-sm text-muted-foreground">Tells the CLI exactly where every file lives for precision installs.</p>
      </div>
      <div class="space-y-2">
        <ZapIcon class="w-5 h-5 text-primary" />
        <h3 class="font-semibold">Context Aware</h3>
        <p class="text-sm text-muted-foreground">Provides instant suggestions for the right component in the right scenario.</p>
      </div>
      <div class="space-y-2">
        <BookOpenIcon class="w-5 h-5 text-primary" />
        <h3 class="font-semibold">Discoverable</h3>
        <p class="text-sm text-muted-foreground">No hunting through folders; everything is listed in one organized source.</p>
      </div>
    </section>

    <Separator />

    <section class="space-y-6">
      <div class="space-y-2">
        <h2 id="analogy" class="text-2xl font-bold">The Blueprint</h2>
        <p class="text-muted-foreground">
          Think of <code class="bg-muted px-1 rounded text-primary">registry.json</code> as a restaurant menu. 
          Instead of searching the kitchen for ingredients, you refer to a single document that lists every dish with its details.
        </p>
      </div>

      <div class="rounded-lg border bg-zinc-950 overflow-hidden">
        <CodeBlock :hideheading="true" :code="registryJson" />
      </div>
    </section>

    <section class="space-y-6">
      <h2 id="regformat" class="text-2xl font-bold">Registry Schema</h2>
      <div class="grid gap-4 border-l-2 border-muted pl-6">
        <div v-for="field in registryFields" :key="field.key" class="space-y-1">
          <code class="text-sm font-bold text-primary uppercase tracking-wider">{{ field.key }}</code>
          <p class="text-muted-foreground text-sm">{{ field.desc }}</p>
        </div>
      </div>
    </section>

    <Card class="bg-muted/30 border-dashed">
      <CardContent class="pt-6 flex items-center justify-between">
        <div>
          <h2 id="liveregcount" class="text-lg font-semibold">Live Registry Stats</h2>
          <p class="text-sm text-muted-foreground">Total components currently mapped in production.</p>
        </div>
        <div class="text-4xl font-black text-primary">
          {{ totalComponents }}
        </div>
      </CardContent>
    </Card>
  </div>
</template>