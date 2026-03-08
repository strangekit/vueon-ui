<template>
  <section class="py-16 px-6 max-w-6xl mx-auto space-y-14">
  
    <!-- Header -->
    <div class="text-center space-y-3">
      <h1 class="text-4xl font-bold text-primary">Vueon UI – Live Demo</h1>
      <p class="text-muted-foreground">
        Minimal interactive clusters built with Vueon components.
      </p>
    </div>
  
    <!-- Grid -->
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
  
      <!-- Loading Card -->
      <Card>
        <CardHeader>
          <CardTitle>Loading State</CardTitle>
          <CardDescription>Skeleton preview</CardDescription>
        </CardHeader>
  
        <CardContent class="space-y-4">
          <div class="flex items-center gap-3">
            <SkeletonCircle />
            <SkeletonText :lines="2" class="w-full"/>
          </div>
  
          <Skeleton class="h-32 w-full rounded-md"/>
        </CardContent>
  
        <CardFooter>
          <Button class="w-full">Reload</Button>
        </CardFooter>
      </Card>
  
  
      <!-- Social Post -->
      <Card class="space-y-3 p-4">
        <div class="flex items-center gap-3">
          <Avatar size="lg" src="/avatar_imgs/avatar_1.jpg"/>
          <div>
            <p class="font-semibold text-sm">Rishabh Jain</p>
            <p class="text-xs text-muted-foreground">@rushabh · 2h</p>
          </div>
        </div>
  
        <p class="text-sm">
          Building Vueon UI all night 😭🔥
        </p>
  
        <Skeleton class="h-40 w-full rounded-lg"/>
  
        <div class="flex gap-3 pt-1">
  
          <Toggle class="group data-[state=on]:text-red-500">
            <Heart class="w-4 h-4 group-data-[state=on]:fill-red-500"/>
          </Toggle>
  
          <Toggle class="group data-[state=on]:text-blue-500">
            <Bookmark class="w-4 h-4 group-data-[state=on]:fill-blue-500"/>
          </Toggle>
  
          <Drawer>
            <DrawerTrigger>
              <Button variant="ghost" size="sm">
                <MessageCircle class="w-4 h-4"/>
              </Button>
            </DrawerTrigger>
  
            <DrawerContent>
              <DrawerHeader>
                <DrawerTitle>Comments</DrawerTitle>
                <DrawerDescription>Join the discussion</DrawerDescription>
              </DrawerHeader>
  
              <div class="p-4 space-y-3">
                <Input placeholder="Write a comment"/>
                <Button class="w-full">Post Comment</Button>
              </div>
            </DrawerContent>
          </Drawer>
  
        </div>
      </Card>
  
  
      <!-- Search + Switch -->
      <Card>
        <CardHeader>
          <CardTitle>Quick Controls</CardTitle>
        </CardHeader>
  
        <CardContent class="space-y-4">
  
          <div class="flex items-center border rounded-xl px-2">
            <SearchIcon class="w-5 h-5 text-muted-foreground"/>
            <Input
              v-model="query"
              placeholder="Search..."
              class="border-none focus-visible:ring-0"
            />
            <Button variant="ghost">
              <SendHorizontal class="w-4 h-4"/>
            </Button>
          </div>
  
          <Separator/>
  
          <div class="flex items-center justify-between">
            <Label>Airplane Mode</Label>
            <Switch v-model="airplaneMode"/>
          </div>
  
          <div class="flex items-center gap-3">
            <Indicator value="2" relativeMode rounded>
              <Avatar size="lg" src="/avatar_imgs/avatar_1.jpg"/>
            </Indicator>
  
            <div>
              <p>@jonTheDon</p>
              <p class="text-xs text-muted-foreground">online</p>
            </div>
          </div>
  
        </CardContent>
      </Card>
  
  
      <!-- OTP Auth -->
      <Card>
        <CardHeader>
          <CardTitle>2FA Verification</CardTitle>
          <CardDescription>Enter the code</CardDescription>
        </CardHeader>
  
        <CardContent class="space-y-4">
  
          <OtpField v-model="otp" :length="6"/>
  
          <Button class="w-full">
            Verify
          </Button>
  
          <p class="text-xs text-muted-foreground text-center">
            Resend code in {{ timer }}s
          </p>
  
        </CardContent>
      </Card>
  
  
      <!-- Simple Form -->
      <Card>
        <CardHeader>
          <CardTitle>Profile Settings</CardTitle>
        </CardHeader>
  
        <CardContent class="space-y-3">
  
          <Input label="Username"/>
          <Input label="Favorite Song"/>
  
          <Label>Age</Label>
          <NumberField :min="1" :max="120"/>
  
          <Button class="w-full mt-3">
            Save Changes
          </Button>
  
        </CardContent>
      </Card>
  
  
      <!-- Buttons -->
      <Card>
        <CardHeader>
          <CardTitle>Button Variants</CardTitle>
        </CardHeader>
  
        <CardContent class="flex gap-2 flex-wrap">
  
          <Button variant="default">
            <PandaIcon class="w-4 h-4"/>
          </Button>
  
          <Button variant="outline">
            <RabbitIcon class="w-4 h-4"/>
          </Button>
  
          <Button variant="ghost">
            <SquirrelIcon class="w-4 h-4"/>
          </Button>
  
          <Button variant="destructive">
            <BugIcon class="w-4 h-4"/>
          </Button>
  
        </CardContent>
      </Card>
  
    </div>
  
  </section>
  </template>
  
  
  <script setup lang="ts">
  import { ref, onMounted, onUnmounted } from "vue"
  
  import { Button } from "../ui/Button"
  import Input from "../ui/Input"
  import { Card, CardHeader, CardTitle, CardDescription, CardContent, CardFooter } from "../ui/Card"
  import { Skeleton, SkeletonCircle, SkeletonText } from "../ui/Skeleton"
  import Switch from "../ui/Switch"
  import Label from "../ui/Label"
  import Toggle from "../ui/Toggle"
  import NumberField from "../ui/NumberField"
  import Indicator from "../ui/Indicator"
  
  import Separator from "../ui/Separator"
  import Avatar from "../ui/Avatar"
  import { Drawer, DrawerTrigger, DrawerContent, DrawerHeader, DrawerTitle, DrawerDescription } from "../ui/Drawer"
  import OtpField from "../ui/OtpField"
  
  import {
    Heart,
    Bookmark,
    MessageCircle,
    SearchIcon,
    SendHorizontal,
    PandaIcon,
    RabbitIcon,
    SquirrelIcon,
    BugIcon
  } from "lucide-vue-next"
  
  const query = ref("")
  const airplaneMode = ref(false)
  const otp = ref("")
  
  const timer = ref(30)
  let interval: number
  
  onMounted(() => {
    interval = setInterval(() => {
      if (timer.value > 0) timer.value--
    }, 1000)
  })
  
  onUnmounted(() => {
    clearInterval(interval)
  })
  </script>