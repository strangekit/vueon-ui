<script setup lang="ts">
import { ref } from "vue";
import CodeBlock from "../../components/CodeBlock.vue";
import DocsNavigation from "../../components/DocsNavigation.vue";
import Separator from "../../components/ui/Separator";
import { FileCode2Icon, Settings2Icon } from "lucide-vue-next";

const schemaRaw = `{
  "$schema": "https://vueonui.com/schema.json",
  "framework": "vue-vite",
  "paths": {
    "components": "./src/components",
    "css": "./src/assets/index.css"
  },
  "tailwind": {
    "config": "tailwind.config.js",
    "css": "path to your css",
    "baseColor": "zinc"
  },
  "aliases": {
    "components": "@/components",
    "ui": "@/ui",
    "lib": "@/lib"
  },
  "iconLibrary": "lucide"
}`;

const schemaFields = [
  { name: "theme", desc: "Color system and design tokens (like Tailwind OKLCH)." },
  { name: "framework", desc: "Which JS framework your project uses (e.g., Vue, Nuxt)." },
  { name: "paths", desc: "The internal directory mapping for components and assets." },
  { name: "tailwind", desc: "Configuration for your Tailwind CSS environment and base colors." },
  { name: "aliases", desc: "Import aliases used to resolve paths in your project." },
  { name: "iconLibrary", desc: "Defines the default icon set (e.g., Lucide, Radix)." },
];

const schemaExample = ref(schemaRaw);
</script>

<template>
  <section class="space-y-10 max-w-4xl pb-20">
    <DocsNavigation
      :prev="{ title: 'Blocks', path: '/docs/blocks' }"
      :next="{ title: 'Theming', path: '/docs/theming' }"
    />

    <header class="space-y-3">
    
      <h1 id="schema" class="text-4xl font-extrabold tracking-tight text-foreground">Project Schema</h1>
      <p class="text-lg text-muted-foreground leading-relaxed max-w-2xl">
        Define the metadata for your project. This configuration allows the CLI and components to resolve paths and styles automatically.
      </p>
    </header>

    <div class="rounded-xl border border-border/50 overflow-hidden shadow-sm">
      <CodeBlock
        :hideheading="true"
        :code="schemaExample"
      />
    </div>

    <section class="space-y-6">
      <div class="space-y-1">
        <h2 id="schemafields" class="text-2xl font-bold tracking-tight">Schema Fields</h2>
        <p class="text-sm text-muted-foreground">Detailed breakdown of the configuration keys.</p>
      </div>
      
      <Separator />

      <div class="grid gap-8">
        <div v-for="field in schemaFields" :key="field.name" class="group">
          <div class="flex flex-col md:flex-row md:items-baseline gap-1 md:gap-4">
            <code class="text-primary font-bold text-base bg-primary/5 px-2 py-0.5 rounded border border-primary/10 w-fit">
              "{{ field.name }}"
            </code>
            <p class="text-muted-foreground text-sm leading-relaxed group-hover:text-foreground transition-colors">
              {{ field.desc }}
            </p>
          </div>
        </div>
      </div>
    </section>

    <div class="p-6 rounded-2xl border bg-muted/30 border-dashed">
      <p class="text-sm leading-relaxed italic text-muted-foreground">
        <strong>Tip:</strong> You can place this file in your root directory. The CLI will automatically detect it to handle component generation and path aliasing.
      </p>
    </div>
  </section>
</template>