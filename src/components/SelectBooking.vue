<template>
    <div class="w-full mb-3">
        <Disclosure v-slot="{ open }">
            <DisclosureButton
            :class="open ? 'bg-orange-100' : ''"
            class="flex w-full justify-between border border-orange-500 rounded-lg px-4 py-2 text-left text-sm font-medium text-orange-500 hover:bg-orange-100 focus:outline-none focus-visible:ring focus-visible:ring-orange-500/75"
            >
            <span class="block truncate option-booking-room" :data-room-name="roomName">{{ localSelectOption.time }}</span>
            <span class="text-center">{{ localSelectOption.slots }} slots</span>
            <ChevronUpIcon
                :class="open ? 'rotate-180 transform' : ''"
                class="h-5 w-5 text-orange-500"
            />
            </DisclosureButton>

            <transition
            leave-active-class="transition duration-100 ease-in"
            leave-from-class="opacity-100"
            leave-to-class="opacity-0"
            >
            <DisclosurePanel class="mb-4 text-sm rounded-lg shadow-md text-gray-500">
                <RadioGroup v-model="localSelectOption">
                    <div class="space-y-1">
                        <RadioGroupOption
                            as="template"
                            v-for="item in infoBooking"
                            :key="item.time"
                            :value="item"
                            v-slot="{ active, checked }"
                        >
                            <div
                            :class="[
                                active
                                ? 'ring-2 ring-white/60 ring-offset-2 ring-offset-sky-300'
                                : '',
                                checked ? 'bg-orange-600/75 text-white ' : 'bg-white ',
                            ]"
                            class="relative flex cursor-pointer px-5 py-2 rounded-sm shadow-md focus:outline-none"
                            >
                                <div class="flex w-full items-center">
                                    <div class="flex items-center justify-between w-full text-sm">
                                        <RadioGroupLabel
                                        as="p"
                                        :class="checked ? 'text-white' : 'text-gray-900'"
                                        class="font-medium"
                                        >
                                        {{ item.time }}
                                        </RadioGroupLabel>
                                        <RadioGroupDescription
                                        as="span"
                                        :class="checked ? 'text-sky-100' : 'text-gray-500'"
                                        class="inline"
                                        >
                                        {{ item.slots }} slots
                                        </RadioGroupDescription>
                                        <div v-show="checked" class="shrink-0 text-white">
                                            <svg class="h-6 w-6" viewBox="0 0 24 24" fill="none">
                                                <circle
                                                cx="12"
                                                cy="12"
                                                r="12"
                                                fill="#fff"
                                                fill-opacity="0.2"
                                                />
                                                <path
                                                d="M7 13l3 3 7-7"
                                                stroke="#fff"
                                                stroke-width="1.5"
                                                stroke-linecap="round"
                                                stroke-linejoin="round"
                                                />
                                            </svg>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </RadioGroupOption>
                    </div>
                </RadioGroup>
            </DisclosurePanel>
            </transition>
        </Disclosure>
    </div>
</template>

<script>
import { Disclosure, DisclosureButton, DisclosurePanel, RadioGroupDescription, RadioGroupOption, RadioGroup } from '@headlessui/vue'
import { ChevronUpIcon } from '@heroicons/vue/20/solid'
  
export default {
    name: "SelectBooking",
    components: {
        Disclosure,
        DisclosureButton,
        DisclosurePanel,
        RadioGroup,
        RadioGroupDescription,
        RadioGroupOption,
        ChevronUpIcon
    },
    props: {
        infoBooking: {
            type: Object,
            required: true
        },
        selectOption: {
            type: Object,
            required: true
        },
        roomName: {
            type: String,
            required: true
        },
    },
    data() {
        return {
            localSelectOption: this.selectOption,
        };
    },
    watch: {
        selectOption(newVal) {
            this.localSelectOption = newVal;
        },
        localSelectOption(newVal) {
            this.$emit("update:selectOption", newVal);
        },
    },
}
</script>

<style scoped>

</style>