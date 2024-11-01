<template>
	<div class="bg-white">
		<div class="mx-auto max-w-7xl px-4 py-16 sm:px-6 lg:px-8">
			<h1 class="text-3xl font-bold tracking-tight text-gray-900">
				Culinary Masterpieces
			</h1>
			<p class="mt-4 max-w-xl text-sm text-gray-700">
				Discover our collection of delicious recipes crafted by expert chefs.
				Find the perfect dish for any occasion, from quick weeknight dinners
				to special celebrations.
			</p>
		</div>
	</div>
  <!-- Filters -->
  <section aria-labelledby="filter-heading">
          <h2 id="filter-heading" class="sr-only">Filters</h2>

          <div class="border-b border-gray-200 bg-white pb-4">
            <div class="mx-auto flex max-w-7xl items-center justify-between px-4 sm:px-6 lg:px-8">
              <Menu as="div" class="relative inline-block text-left">
                <div>
                  <MenuButton class="group inline-flex justify-center text-sm font-medium text-gray-700 hover:text-gray-900">
                    Sort
                    <ChevronDownIcon class="-mr-1 ml-1 h-5 w-5 flex-shrink-0 text-gray-400 group-hover:text-gray-500" aria-hidden="true" />
                  </MenuButton>
                </div>

                <transition enter-active-class="transition ease-out duration-100" enter-from-class="transform opacity-0 scale-95" enter-to-class="transform opacity-100 scale-100" leave-active-class="transition ease-in duration-75" leave-from-class="transform opacity-100 scale-100" leave-to-class="transform opacity-0 scale-95">
                  <MenuItems class="absolute left-0 z-10 mt-2 w-40 origin-top-left rounded-md bg-white shadow-2xl ring-1 ring-black ring-opacity-5 focus:outline-none">
                    <div class="py-1">
                      <MenuItem v-for="option in sortOptions" :key="option.name" v-slot="{ active }">
                        <a :href="option.href" :class="[option.current ? 'font-medium text-gray-900' : 'text-gray-500', active ? 'bg-gray-100' : '', 'block px-4 py-2 text-sm']">{{ option.name }}</a>
                      </MenuItem>
                    </div>
                  </MenuItems>
                </transition>
              </Menu>

              <button type="button" class="inline-block text-sm font-medium text-gray-700 hover:text-gray-900 sm:hidden" @click="mobileFiltersOpen = true">Filters</button>

              <div class="hidden sm:block">
                <div class="flow-root">
                  <PopoverGroup class="-mx-4 flex items-center divide-x divide-gray-200">
                    <Popover v-for="(section, sectionIdx) in filters" :key="section.name" class="relative inline-block px-4 text-left">
                      <PopoverButton class="group inline-flex justify-center text-sm font-medium text-gray-700 hover:text-gray-900">
                        <span>{{ section.name }}</span>
                        <span v-if="sectionIdx === 0" class="ml-1.5 rounded bg-gray-200 px-1.5 py-0.5 text-xs font-semibold tabular-nums text-gray-700">1</span>
                        <ChevronDownIcon class="-mr-1 ml-1 h-5 w-5 flex-shrink-0 text-gray-400 group-hover:text-gray-500" aria-hidden="true" />
                      </PopoverButton>

                      <transition enter-active-class="transition ease-out duration-100" enter-from-class="transform opacity-0 scale-95" enter-to-class="transform opacity-100 scale-100" leave-active-class="transition ease-in duration-75" leave-from-class="transform opacity-100 scale-100" leave-to-class="transform opacity-0 scale-95">
                        <PopoverPanel class="absolute right-0 z-10 mt-2 origin-top-right rounded-md bg-white p-4 shadow-2xl ring-1 ring-black ring-opacity-5 focus:outline-none">
                          <form class="space-y-4">
                            <div v-for="(option, optionIdx) in section.options" :key="option.value" class="flex items-center">
                              <input :id="`filter-${section.id}-${optionIdx}`" :name="`${section.id}[]`" :value="option.value" type="checkbox" :checked="option.checked" class="h-4 w-4 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500" />
                              <label :for="`filter-${section.id}-${optionIdx}`" class="ml-3 whitespace-nowrap pr-6 text-sm font-medium text-gray-900">{{ option.label }}</label>
                            </div>
                          </form>
                        </PopoverPanel>
                      </transition>
                    </Popover>
                  </PopoverGroup>
                </div>
              </div>
            </div>
          </div>

          <!-- Active filters -->
          <div class="bg-gray-100">
            <div class="mx-auto max-w-7xl px-4 py-3 sm:flex sm:items-center sm:px-6 lg:px-8">
              <h3 class="text-sm font-medium text-gray-500">
                Filters
                <span class="sr-only">, active</span>
              </h3>

              <div aria-hidden="true" class="hidden h-5 w-px bg-gray-300 sm:ml-4 sm:block" />

              <div class="mt-2 sm:ml-4 sm:mt-0">
                <div class="-m-1 flex flex-wrap items-center">
                  <span v-for="activeFilter in activeFilters" :key="activeFilter.value" class="m-1 inline-flex items-center rounded-full border border-gray-200 bg-white py-1.5 pl-3 pr-2 text-sm font-medium text-gray-900">
                    <span>{{ activeFilter.label }}</span>
                    <button type="button" class="ml-1 inline-flex h-4 w-4 flex-shrink-0 rounded-full p-1 text-gray-400 hover:bg-gray-200 hover:text-gray-500">
                      <span class="sr-only">Remove filter for {{ activeFilter.label }}</span>
                      <svg class="h-2 w-2" stroke="currentColor" fill="none" viewBox="0 0 8 8">
                        <path stroke-linecap="round" stroke-width="1.5" d="M1 1l6 6m0-6L1 7" />
                      </svg>
                    </button>
                  </span>
                </div>
              </div>
            </div>
          </div>
        </section>

        <!-- Product grid -->
        <section aria-labelledby="products-heading" class="mx-auto max-w-2xl px-4 pb-16 pt-12 sm:px-6 sm:pb-24 sm:pt-16 lg:max-w-7xl lg:px-8">
          <h2 id="products-heading" class="sr-only">Products</h2>

          <div class="grid grid-cols-1 gap-x-6 gap-y-10 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 xl:gap-x-8">
            <a v-for="product in products" :key="product.id" :href="product.href" class="group">
              <div class="aspect-h-1 aspect-w-1 w-full overflow-hidden rounded-lg bg-gray-200 xl:aspect-h-8 xl:aspect-w-7">
                <img :src="product.imageSrc" :alt="product.imageAlt" class="h-full w-full object-cover object-center group-hover:opacity-75" />
              </div>
              <h3 class="mt-4 text-sm text-gray-700">{{ product.name }}</h3>
              <p class="mt-1 text-lg font-medium text-gray-900">{{ product.price }}</p>
            </a>
          </div>
        </section>
</template>
<script setup>
import { Menu, MenuButton, MenuItem, MenuItems } from '@headlessui/vue'
import { ChevronDownIcon } from '@heroicons/vue/20/solid'
import { Popover, PopoverButton, PopoverGroup, PopoverPanel } from '@headlessui/vue'

const sortOptions = [
  { name: 'Most Popular', href: '#', current: true },
  { name: 'Best Rating', href: '#', current: false },
  { name: 'Newest', href: '#', current: false },
]

const filters = [
  {
    id: 'category',
    name: 'Category',
    options: [
      { value: 'breakfast', label: 'Breakfast', checked: false },
      { value: 'lunch', label: 'Lunch', checked: false },
      { value: 'dinner', label: 'Dinner', checked: true },
      { value: 'dessert', label: 'Dessert', checked: false },
    ],
  },
  {
    id: 'difficulty',
    name: 'Difficulty',
    options: [
      { value: 'easy', label: 'Easy', checked: false },
      { value: 'medium', label: 'Medium', checked: false },
      { value: 'hard', label: 'Hard', checked: true },
    ],
  },
  {
    id: 'time',
    name: 'Time',
    options: [
      { value: '15min', label: '15 minutes or less', checked: false },
      { value: '30min', label: '30 minutes or less', checked: true },
      { value: '45min', label: '45 minutes or less', checked: false },
      { value: '1hour', label: '1 hour or less', checked: false },
    ],
  },
]

const activeFilters = [
  { value: 'dinner', label: 'Dinner' },
  { value: 'hard', label: 'Hard' },
  { value: '30min', label: '30 minutes or less' },
]

const products = [
  {
    id: 1,
    name: 'Grilled Salmon',
    href: '#',
    imageSrc: 'https://images.unsplash.com/photo-1519708227418-c8fd9a32b7a2?h=1000&w=750&fit=crop',
    imageAlt: "Grilled salmon with vegetables",
    price: '30 minutes',
    servings: '4 servings'
  },
  {
    id: 2, 
    name: 'Pasta Carbonara',
    href: '#',
    imageSrc: 'https://images.unsplash.com/photo-1546549032-9571cd6b27df?h=1000&w=750&fit=crop',
    imageAlt: "Classic pasta carbonara",
    price: '25 minutes',
    servings: '6 servings'
  },
  {
    id: 3,
    name: 'Chicken Stir Fry',
    href: '#',
    imageSrc: 'https://images.unsplash.com/photo-1555939594-58d7cb561ad1?h=1000&w=750&fit=crop',
    imageAlt: "Chicken stir fry with vegetables",
    price: '20 minutes',
    servings: '4 servings'
  },
  {
    id: 4,
    name: 'Beef Tacos',
    href: '#',
    imageSrc: 'https://images.unsplash.com/photo-1504544750208-dc0358e63f7f?h=1000&w=750&fit=crop',
    imageAlt: "Beef tacos with fresh toppings",
    price: '35 minutes',
    servings: '6 servings'
  },
  {
    id: 5,
    name: 'Vegetable Curry',
    href: '#', 
    imageSrc: 'https://images.unsplash.com/photo-1455619452474-d2be8b1e70cd?h=1000&w=750&fit=crop',
    imageAlt: "Spicy vegetable curry with rice",
    price: '40 minutes',
    servings: '4 servings'
  },
  {
    id: 6,
    name: 'Homemade Pizza',
    href: '#',
    imageSrc: 'https://images.unsplash.com/photo-1513104890138-7c749659a591?h=1000&w=750&fit=crop',
    imageAlt: "Fresh homemade margherita pizza",
    price: '45 minutes',
    servings: '8 servings'
  },
  {
    id: 7,
    name: 'Greek Salad',
    href: '#',
    imageSrc: 'https://images.unsplash.com/photo-1540189549336-e6e99c3679fe?h=1000&w=750&fit=crop',
    imageAlt: "Traditional Greek salad with feta",
    price: '15 minutes',
    servings: '4 servings'
  },
  {
    id: 8,
    name: 'Beef Burger',
    href: '#',
    imageSrc: 'https://images.unsplash.com/photo-1568901346375-23c9450c58cd?h=1000&w=750&fit=crop',
    imageAlt: "Juicy beef burger with toppings",
    price: '25 minutes',
    servings: '4 servings'
  },
  {
    id: 9,
    name: 'Mushroom Risotto',
    href: '#',
    imageSrc: 'https://images.unsplash.com/photo-1476124369491-e7addf5db371?h=1000&w=750&fit=crop',
    imageAlt: "Creamy mushroom risotto",
    price: '35 minutes',
    servings: '6 servings'
  },
  {
    id: 10,
    name: 'Chocolate Cake',
    href: '#',
    imageSrc: 'https://images.unsplash.com/photo-1578985545062-69928b1d9587?h=1000&w=750&fit=crop',
    imageAlt: "Rich chocolate layer cake",
    price: '50 minutes',
    servings: '12 servings'
  },
]

</script>
