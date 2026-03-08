<script setup lang="ts">
import { ArrowRight } from 'lucide-vue-next';
import { Card, CardContent, CardFooter, CardHeader } from '../../components/ui/Card';
import { Button } from '../../components/ui/Button';
import DocsNavigation from '../../components/DocsNavigation.vue';
</script>

<template>
  <div class="space-y-10 max-w-5xl">
    <DocsNavigation
      :prev="{ title: 'Getting Started', path: '/docs' }"
      :next="{ title: 'Theming', path: '/docs/theming' }"
    />

    <header class="space-y-2">
      <h1 id="installation" class="text-3xl font-bold tracking-tight">Installation</h1>
      <p class="text-muted-foreground text-lg">
        Choose your framework below to install Vueon UI.
      </p>
    </header>

    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
      
      <Card class="flex flex-col group transition-all hover:border-primary/40">
        <CardHeader class="text-center pb-2">
          <span class="font-semibold text-lg">Vite + Vue3</span>
        </CardHeader>
        <CardContent class="flex-1 flex items-center justify-center p-6">
          <img src="/logos/logo_vite.svg" class="h-14 w-auto  transition-all duration-300" alt="vite" />
        </CardContent>
        <CardFooter class="justify-center pt-0 pb-6">
          <router-link :to="{ name: 'docs-installation-framework', params: { framework: 'vite-vue' } }">
            <Button variant="link" class="gap-2 h-auto p-0 font-medium">
              Check Installation <ArrowRight class="w-4 h-4"/>
            </Button>
          </router-link>
        </CardFooter>
      </Card>

      <Card class="flex flex-col group transition-all hover:border-primary/40">
        <CardHeader class="text-center pb-2">
          <span class="font-semibold text-lg">Vue3</span>
        </CardHeader>
        <CardContent class="flex-1 flex items-center justify-center p-6">
          <img src="/logos/logo_vue.svg" class="h-14 w-auto  transition-all duration-300" alt="vue" />
        </CardContent>
        <CardFooter class="justify-center pt-0 pb-6">
          <router-link :to="{ name: 'docs-installation-framework', params: { framework: 'vue3' } }">
            <Button variant="link" class="gap-2 h-auto p-0 font-medium">
              Check Installation <ArrowRight class="w-4 h-4"/>
            </Button>
          </router-link>
        </CardFooter>
      </Card>

      <Card class="flex flex-col group transition-all hover:border-primary/40">
        <CardHeader class="text-center pb-2">
          <span class="font-semibold text-lg">Nuxt</span>
        </CardHeader>
        <CardContent class="flex-1 flex items-center justify-center p-6">
          <img src="/logos/logo_nuxt.svg" class="h-14 w-auto  transition-all duration-300" alt="nuxt" />
        </CardContent>
        <CardFooter class="justify-center pt-0 pb-6">
          <router-link :to="{ name: 'docs-installation-framework', params: { framework: 'nuxt' } }">
            <Button variant="link" class="gap-2 h-auto p-0 font-medium">
              Check Installation <ArrowRight class="w-4 h-4"/>
            </Button>
          </router-link>
        </CardFooter>
      </Card>

      <Card class="flex flex-col group transition-all hover:border-primary/40">
        <CardHeader class="text-center pb-2">
          <span class="font-semibold text-lg">Laravel</span>
        </CardHeader>
        <CardContent class="flex-1 flex items-center justify-center p-6">
          <img src="/logos/logo_laravel.svg" class="h-14 w-auto transition-all duration-300" alt="laravel" />
        </CardContent>
        <CardFooter class="justify-center pt-0 pb-6">
          <router-link :to="{ name: 'docs-installation-framework', params: { framework: 'laravel' } }">
            <Button variant="link" class="gap-2 h-auto p-0 font-medium">
              Check Installation <ArrowRight class="w-4 h-4"/>
            </Button>
          </router-link>
        </CardFooter>
      </Card>

      <Card class="flex flex-col  group transition-all hover:border-primary/40">
        <CardHeader class="text-center pb-2">
          <span class="font-semibold text-lg">Astro</span>
        </CardHeader>
        <CardContent class="flex-1 flex items-center justify-center p-6">
          <img src="/logos/astro-frame.svg" class="h-14 w-auto  transition-all duration-300" alt="astro" />
        </CardContent>
        <CardFooter class="justify-center pt-0 pb-6">
          <router-link :to="{ name: 'docs-installation-framework', params: { framework: 'astro' } }">
            <Button variant="link" class="gap-2 h-auto p-0 font-medium">
              Check Installation <ArrowRight class="w-4 h-4"/>
            </Button>
          </router-link>
        </CardFooter>
      </Card>

    </div>
  </div>
</template>