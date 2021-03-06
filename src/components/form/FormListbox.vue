<template>
  <Listbox
    as="div"
    class="px-4 pt-2 pb-8 bg-gray-100 border border-gray-100 rounded-md dark:border-gray-800 dark:bg-gray-800 focus-within:bg-white dark:focus-within:bg-gray-900 focus-within:ring-2 focus-within:ring-offset-2 focus-within:ring-offset-white dark:focus-within:ring-offset-gray-900 focus-within:ring-primary-500"
    :modelValue="value"
    v-slot="{ open }"
    @update:modelValue="handleInput"
  >
    <ListboxLabel class="block font-semibold tracking-wide text-gray-500 uppercase transition-all duration-200 ease-in-out transform text-2xs">
      {{ label }}
    </ListboxLabel>

    <ListboxButton class="absolute inset-0 z-10 flex items-center justify-between w-full px-4 mt-px text-left text-gray-900 dark:text-white focus:outline-none focus:ring-0">
      <span class="mt-4">
        {{ options.find(o => o.value === value).label }}
      </span>

      <svg class="w-4 h-4 text-gray-500" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" clip-rule="evenodd" />
      </svg>
    </ListboxButton>

    <transition
      leave-active-class="transition duration-100 ease-in"
      leave-from-class="opacity-100"
      leave-to-class="opacity-0"
    >
      <div
        v-if="open"
        class="absolute z-20 mb-2 bg-white rounded-md shadow-lg -inset-x-px dark:bg-gray-900 bottom-full"
      >
        <ListboxOptions class="overflow-y-auto bg-white border border-gray-100 rounded-md shadow-xs max-h-60 dark:bg-gray-900 focus:outline-none dark:border-gray-800">
          <ListboxOption
            v-for="option in options"
            :key="option.value"
            class="w-full focus:outline-none focus:ring-0"
            :value="option.value"
            v-slot="{ selected, active }"
          >
            <button
              class="flex items-center justify-between w-full px-4 py-2 focus:outline-none focus:ring-0"
              :class="{
                'bg-gray-100 dark:bg-gray-800 text-gray-900 dark:text-white': active,
                'font-semibold text-gray-900 dark:text-white': selected,
                'text-gray-600 dark:text-gray-400': !selected && !active,
              }"
            >
              {{ option.label }}

              <svg
                v-if="selected"
                class="w-4 h-4 ml-4"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 20 20"
                fill="currentColor"
              >
                <path
                  fill-rule="evenodd"
                  d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"
                  clip-rule="evenodd"
                />
              </svg>
            </button>
          </ListboxOption>
        </ListboxOptions>
      </div>
    </transition>
  </Listbox>
</template>

<script>
import {
  Listbox,
  ListboxButton,
  ListboxLabel,
  ListboxOption,
  ListboxOptions,
} from '@headlessui/vue'

export default {
  props: ['label', 'options', 'value'],
  components: {
    Listbox,
    ListboxButton,
    ListboxLabel,
    ListboxOption,
    ListboxOptions,
  },
  setup(_, { emit }) {
    const handleInput = (v) => emit('update:value', v)

    return {
      handleInput,
    }
  },
}
</script>
