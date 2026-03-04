<script setup lang="ts">
import { BatteryFullIcon, InboxIcon, RabbitIcon } from 'lucide-vue-next';
import { Button } from './components/Button';
import { Chain,  ChainContent, ChainDescription, ChainAction, ChainHeader } from './components/Chain';
import ChainGroup from './components/Chain/ChainGroup.vue';
import ChainMeta from './components/Chain/ChainMeta.vue';
import Separator from './components/Separator';
import { SlideAction  } from './components/SlideAction';
// import { Button } from './components/Button';
import { 
  AlertDialog,
  AlertDialogTrigger,
  AlertDialogContent,
  AlertDialogHeader,
  AlertDialogFooter,
  AlertDialogTitle,
  AlertDialogDescription,
  AlertDialogCancel,
  AlertDialogAction
} from "./components/AlertDialog"
import Calendar from './components/Calendar/Calendar.vue';
import Label from './components/Label/Label.vue';
import Checkbox from './components/Checkbox/Checkbox.vue';

import {
  Collapsible,
  CollapsibleTrigger,
  CollapsibleContent
} from "./components/Collapsible"
import {
  Menubar,
  MenubarMenu,
  MenubarTrigger,
  MenubarContent,
  MenubarItem,
  MenubarLabel,
  MenubarSeparator,
  MenubarCheckboxItem,
  MenubarItemIndicator,
  MenubarRadioGroup,
  MenubarRadioItem,
  MenubarSub,
  MenubarSubTrigger,
  MenubarSubContent,
  MenubarArrow
} from "./components/Menubar"
import { Check, Circle, ChevronRight } from "lucide-vue-next"
import { ref } from "vue"
const toolbar = ref(true)
const theme = ref("light")


// Selected value
const selectedFood = ref('')
// Options array
const foodOptions = [
  {
    name: 'Fruit',
    children: [
      { name: 'Apple' },
      { name: 'Banana' },
      { name: 'Orange' },
      { name: 'Grapes' }
    ]
  },
  {
    name: 'Vegetable',
    children: [
      { name: 'Carrot' },
      { name: 'Spinach' },
      { name: 'Potato' },
    ]
  }
]

import ComboBox from './components/ComboBox';


import DateField from './components/DateField';
import GroupDateField from './components/GroupDateField';
import Indicator from './components/Indicator/Indicator.vue';
import NumberField from './components/NumberField';

const otp = ref("");
import OtpField from "@/components/OtpField";


import {
  Popover,
  PopoverTrigger,
  PopoverPortal,
  PopoverContent,
  PopoverClose,
  PopoverArrow,
} from "@/components/Popover";

import { RadioGroup, RadioGroupItem } from './components/RadioGroup'
const selected = ref('a')


import {
  Stepper,
  StepperItem,
  StepperTrigger,
  StepperIndicator,
  StepperTitle,
  StepperDescription,
  StepperSeparator
} from "./components/Stepper"
import { Truck, CreditCard, CheckCircle } from 'lucide-vue-next'

type Step = {
  step: number
  title: string
  description: string
  icon: any
}
// Steps preview
const steps: Step[] = [
  { step: 2, title: "Shipping", description: "Provide shipping info", icon: Truck },
  { step: 3, title: "Payment", description: "Confirm payment method", icon: CreditCard },
  { step: 4, title: "Finish", description: "Complete your order", icon: CheckCircle }
];
</script>

<template>

<!-- <section class="border h-lvh flex gap-2 items-center justify-center"> -->
  <Stepper orientation="horizontal" :default-value="2" class="flex flex-row gap-1 h-lvh w-full max-w-3xl">
          <StepperItem
            v-for="item in steps"
            :key="item.step"
            :step="item.step"
            class="flex items-center !gap-1 cursor-pointer group relative flex-1"
          >
            <!-- Step circle with icon -->
            <StepperTrigger class="w-14">
              <StepperIndicator>
                <component
                    :is="item.icon"
                    class="w-4 h-4 text-primary group-data-[state=active]:text-white group-data-[state=completed]:text-white"
                    />            
                </StepperIndicator>
            </StepperTrigger>
            <!-- Step text -->
            <div class="flex flex-col items-start w-full">
              <StepperTitle
                class="text-sm font-semibold transition-colors group-data-[state=active]:text-primary"
              >
                {{ item.title }}
              </StepperTitle>
              <StepperDescription class="text-xs w-full text-muted-foreground">
                {{ item.description }}
              </StepperDescription>
            </div>
            <!-- Separator -->
            <StepperSeparator
              v-if="item.step !== steps[steps.length - 1].step"
              class="w-12 h-[1px] bg-border mx-3"
            />
          </StepperItem>
        </Stepper>
<!-- </section> -->
        <section class="border h-lvh flex flex-col gap-2 items-center justify-center">
          <RadioGroup v-model="selected">
                <div class="flex items-center gap-3">
                  <RadioGroupItem id="r1" value="a" />
                  <Label for="r1">Default</Label>
                </div>
                <div class="flex items-center gap-3">
                  <RadioGroupItem id="r2" value="b" />
                  <Label for="r2">Option B</Label>
                </div>
              </RadioGroup>
        </section>
<section class="border h-lvh flex flex-col gap-2 items-center justify-center">
  <Popover>
    <PopoverTrigger>
      <Button>
        Open Popover
      </Button>
    </PopoverTrigger>
    <PopoverPortal>
      <PopoverContent class="relative flex flex-col space-y-2">
        <h3 class="text-sm font-semibold">Popover Title</h3>
        <p class="text-sm text-muted-foreground">
          This is a Shadcn-style Popover built with Vueon-UI.
        </p>
        <PopoverClose>
          <Button variant="outline" size="sm">
            Close
          </Button>
        </PopoverClose>
        <PopoverArrow />
      </PopoverContent>
    </PopoverPortal>
  </Popover>
</section>
<section class="border h-lvh flex flex-col gap-2 items-center justify-center">
  <h1 class="text-2xl font-semibold mb-6">OTP Verification</h1>
  <OtpField v-model="otp" :length="4" />
  <hr>
  <OtpField v-model="otp" :length="6" variant="capsule" />
  <hr>
  <OtpField v-model="otp" :length="6" variant="grouped" />
  <p class="mt-4 text-sm text-muted-foreground">
    Entered OTP: <span class="font-medium text-primary">{{ otp }}</span>
  </p>
</section>
<section class="border h-lvh flex flex-col gap-2 items-center justify-center">
  <div class="p-6 flex flex-col gap-6">
    <NumberField label="Age" layout="left" />
    <NumberField label="Quantity" layout="center" />
    <NumberField label="Items" layout="right" />
  </div>
  </section>

<section class="border h-lvh flex  gap-2 items-center justify-center">
  <Menubar>
    <MenubarMenu>
      <MenubarTrigger>File</MenubarTrigger>
      <MenubarContent>
        <MenubarLabel>File</MenubarLabel>
        <MenubarItem>New File</MenubarItem>
        <MenubarItem>Open...</MenubarItem>
        <MenubarSeparator />
        <MenubarSub>
          <MenubarSubTrigger>
            Export
            <ChevronRight class="ml-auto h-4 w-4" />
          </MenubarSubTrigger>
          <MenubarSubContent>
            <MenubarItem>PDF</MenubarItem>
            <MenubarItem>DOCX</MenubarItem>
            <MenubarItem>TXT</MenubarItem>
          </MenubarSubContent>
        </MenubarSub>
      </MenubarContent>
    </MenubarMenu>
  </Menubar>
</section>
<section class="border h-lvh flex flex-col gap-2 items-center justify-center">
  <Indicator  relativeMode rounded size="icon" value="7">
    <InboxIcon />
  </Indicator>
  <Indicator variant="destructive" position="bottom-right" relativeMode rounded size="icon" value="new">
    update
  </Indicator>

 </section> 
<section class="border h-lvh flex flex-col gap-2 items-center justify-center">
  <GroupDateField
    label="Booking Dates"
    id="booking-dates"
    :withPopup="true"
  />
</section>
<section class="border h-lvh flex flex-col gap-2 items-center justify-center">
  <DateField
  withPopup
  label='Birthday'
  :is-date-unavailable='date => date.day === 19'
/>
<DateField
  label='Birthday'
/>
</section>


<section class="border h-lvh flex items-center justify-center">
  <ComboBox
    v-model="selectedFood"
    :options="foodOptions"
    placeholder="Select a food"
/>
</section>
<section class="border h-lvh flex items-center justify-center">
  <div class="w-72">

  <Collapsible>
    <CollapsibleTrigger>
      @peduarte starred 3 repositories
    </CollapsibleTrigger>
    <div class="mt-2 p-2 border rounded-md bg-background shadow-sm text-muted-foreground">
      @radix-ui/primitives
    </div>
    <CollapsibleContent>
      <div class="mt-2 p-2 border rounded-md bg-background shadow-sm text-muted-foreground">
        @vuejs/core
      </div>
      <div class="mt-2 p-2 border rounded-md bg-background shadow-sm text-muted-foreground">
        @reka-ui/primitives
      </div>
    </CollapsibleContent>
  </Collapsible>
</div>

</section>
<section class="border h-lvh flex items-center justify-center">
  <div class="flex items-center space-x-2">
    <Checkbox id="terms" />
    <Label for="terms">Accept terms</Label>
  </div>
</section>
<section class="border h-lvh flex items-center justify-center">
  <Calendar mode='range' />

</section>
<section class="border h-lvh flex items-center justify-center">
  <Calendar />
</section>

<section class="border h-lvh flex items-center justify-center">
  <AlertDialog>
    <AlertDialogTrigger>
      <Button variant="outline">Show Dialog</Button>
    </AlertDialogTrigger>
    <AlertDialogContent>
      <AlertDialogHeader>
        <AlertDialogTitle>Are you absolutely sure?</AlertDialogTitle>
        <AlertDialogDescription>
          This action cannot be undone. It will permanently delete your account.
        </AlertDialogDescription>
      </AlertDialogHeader>
      <AlertDialogFooter>
        <AlertDialogCancel>Cancel</AlertDialogCancel>
        <AlertDialogAction>Continue</AlertDialogAction>
      </AlertDialogFooter>
    </AlertDialogContent>
  </AlertDialog>
</section>

<section class="border h-lvh flex items-center justify-center">
<Button class="" variant="default" size="lg">Primary</Button>
</section>
  <section class="border h-lvh flex items-center justify-center">

    <div class="w-96">
      <SlideAction
      class=""
      :initial-icon="RabbitIcon" 
      :complete-icon="BatteryFullIcon"
      initial-text="pay $32"
      complete-text="paid"
      >
       
      </SlideAction>
    </div>

  </section>
  <!-- <section class="border h-lvh flex items-center justify-center">

<ChainGroup>
  <Chain state="active" dot="top">
    <ChainMeta>28/11/2025</ChainMeta>

    <ChainContent>
      <ChainHeader>Drift</ChainHeader>
      <ChainDescription>
        A draggable component for free, vertical, or horizontal movement.
      </ChainDescription>
      <Separator/>
      <ChainAction>
        <RouterLink to="/docs/components/drift">
          <Button variant="link">View Docs →</Button>
        </RouterLink>
      </ChainAction>
    </ChainContent>
  </Chain>

  <Chain state="active" dot="top">
    <ChainMeta>28/11/2025</ChainMeta>
    <ChainContent>
      <ChainHeader>Highlighter</ChainHeader>
      <ChainDescription>
        A design-system-ready text emphasis component.
      </ChainDescription>
    </ChainContent>
  </Chain>
</ChainGroup>

</section> -->




</template>

<style>
  /* [data-slide-complete="true"] {
  background-color: #22c55e; 
} */
</style>