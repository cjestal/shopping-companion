<template>
	<div class="bg-white">
		<div class="mx-auto max-w-7xl sm:px-6 sm:pt-16 lg:px-8">
			<div class="mx-auto max-w-2xl lg:max-w-none">
				<!-- Recipe -->
				<div class="lg:grid lg:grid-cols-2 lg:items-start lg:gap-x-8">
					<!-- Image gallery -->
					<TabGroup as="div" class="flex flex-col-reverse">
						<!-- Image selector -->
						<div class="mx-auto mt-6 hidden w-full max-w-2xl sm:block lg:max-w-none">
							<TabList class="grid grid-cols-4 gap-6">
								<Tab
									v-for="image in recipe.images" 
									:key="image.id"
									class="relative flex h-24 cursor-pointer items-center justify-center rounded-md bg-white text-sm font-medium uppercase text-gray-900 hover:bg-gray-50 focus:outline-none focus:ring focus:ring-opacity-50 focus:ring-offset-4"
									v-slot="{ selected }"
								>
									<span class="sr-only">{{ image.name }}</span>
									<span class="absolute inset-0 overflow-hidden rounded-md">
										<img
											:src="image.src"
											alt=""
											class="h-full w-full object-cover object-center"
										/>
									</span>
									<span
										:class="[
											selected ? 'ring-red-500' : 'ring-transparent',
											'pointer-events-none absolute inset-0 rounded-md ring-2 ring-offset-2',
										]"
										aria-hidden="true"
									/>
								</Tab>
							</TabList>
						</div>

						<TabPanels class="aspect-h-1 aspect-w-1 w-full">
							<TabPanel v-for="image in recipe.images" :key="image.id">
								<img
									:src="image.src"
									:alt="image.alt"
									class="h-full w-full object-cover object-center sm:rounded-lg"
								/>
							</TabPanel>
						</TabPanels>
					</TabGroup>

					<!-- Recipe info -->
					<div class="mt-10 px-4 sm:mt-16 sm:px-0 lg:mt-0">
						<h1 class="text-3xl font-bold tracking-tight text-gray-900">
							{{ recipe.name }}
						</h1>

						<div class="mt-3">
							<h2 class="sr-only">Recipe information</h2>
							<p class="text-lg tracking-tight text-gray-600">
								{{ recipe.cookTime }} | {{ recipe.servings }} servings
							</p>
						</div>

						<!-- Reviews -->
						<div class="mt-3">
							<h3 class="sr-only">Reviews</h3>
							<div class="flex items-center">
								<div class="flex items-center">
									<StarIcon
										v-for="rating in [0, 1, 2, 3, 4]"
										:key="rating"
										:class="[
											recipe.rating > rating ? 'text-red-500' : 'text-gray-300',
											'h-5 w-5 flex-shrink-0',
										]"
										aria-hidden="true"
									/>
								</div>
								<p class="sr-only">{{ recipe.rating }} out of 5 stars</p>
							</div>
						</div>

						<div class="mt-6">
							<h3 class="sr-only">Description</h3>
							<div class="space-y-6 text-base text-gray-700" v-html="recipe.description" />
						</div>

						<div class="mt-6">
							<h3 class="text-lg font-medium text-gray-900">Ingredients</h3>
							<div class="mt-4">
								<ul role="list" class="list-disc pl-4 space-y-2">
									<li v-for="ingredient in recipe.ingredients" :key="ingredient" class="text-gray-600">
										{{ ingredient }}
									</li>
								</ul>
							</div>
						</div>

						<div class="mt-10 flex">
							<button
								type="button"
								class="flex max-w-xs flex-1 items-center justify-center rounded-md border border-transparent bg-red-600 px-8 py-3 text-base font-medium text-white hover:bg-red-700 focus:outline-none focus:ring-2 focus:ring-red-500 focus:ring-offset-2 focus:ring-offset-gray-50 sm:w-full"
							>
								Add Ingredients to Cart
							</button>

							<button
								type="button"
								class="ml-4 flex items-center justify-center rounded-md px-3 py-3 text-gray-400 hover:bg-gray-100 hover:text-gray-500"
							>
								<HeartIcon class="h-6 w-6 flex-shrink-0" aria-hidden="true" />
								<span class="sr-only">Add to favorites</span>
							</button>
						</div>

						<section aria-labelledby="details-heading" class="mt-12">
							<h2 id="details-heading" class="sr-only">Additional details</h2>

							<div class="divide-y divide-gray-200 border-t">
								<Disclosure
									as="div"
									v-for="(steps, section) in recipe.instructions"
									:key="section"
									v-slot="{ open }"
								>
									<h3>
										<DisclosureButton
											class="group relative flex w-full items-center justify-between py-6 text-left"
										>
											<span
												:class="[
													open ? 'text-red-600' : 'text-gray-900',
													'text-sm font-medium',
												]"
											>{{ section }}</span>
											<span class="ml-6 flex items-center">
												<PlusIcon
													v-if="!open"
													class="block h-6 w-6 text-gray-400 group-hover:text-gray-500"
													aria-hidden="true"
												/>
												<MinusIcon
													v-else
													class="block h-6 w-6 text-red-400 group-hover:text-red-500"
													aria-hidden="true"
												/>
											</span>
										</DisclosureButton>
									</h3>
									<DisclosurePanel as="div" class="prose prose-sm pb-6">
										<ol class="list-decimal pl-4">
											<li v-for="step in steps" :key="step" class="mb-2">
												{{ step }}
											</li>
										</ol>
									</DisclosurePanel>
								</Disclosure>
							</div>
						</section>
					</div>
				</div>

				<section
					aria-labelledby="related-heading"
					class="mt-10 border-t border-gray-200 px-4 py-16 sm:px-0"
				>
					<h2 id="related-heading" class="text-xl font-bold text-gray-900">
						Similar Recipes
					</h2>

					<div
						class="mt-8 grid grid-cols-1 gap-y-12 sm:grid-cols-2 sm:gap-x-6 lg:grid-cols-4 xl:gap-x-8"
					>
						<div v-for="recipe in relatedRecipes" :key="recipe.id">
							<div class="relative">
								<div class="relative h-72 w-full overflow-hidden rounded-lg">
									<img
										:src="recipe.imageSrc"
										:alt="recipe.imageAlt"
										class="h-full w-full object-cover object-center"
									/>
								</div>
								<div class="relative mt-4">
									<h3 class="text-sm font-medium text-gray-900">
										{{ recipe.name }}
									</h3>
									<p class="mt-1 text-sm text-gray-500">
										{{ recipe.cookTime }}
									</p>
								</div>
								<div
									class="absolute inset-x-0 top-0 flex h-72 items-end justify-end overflow-hidden rounded-lg p-4"
								>
									<div
										aria-hidden="true"
										class="absolute inset-x-0 bottom-0 h-36 bg-gradient-to-t from-black opacity-50"
									/>
									<p class="relative text-lg font-semibold text-white">
										{{ recipe.servings }} servings
									</p>
								</div>
							</div>
							<div class="mt-6">
								<a
									:href="recipe.href"
									class="relative flex items-center justify-center rounded-md border border-transparent bg-gray-100 px-8 py-2 text-sm font-medium text-gray-900 hover:bg-gray-200"
								>View Recipe<span class="sr-only">, {{ recipe.name }}</span></a>
							</div>
						</div>
					</div>
				</section>
			</div>
		</div>
	</div>
</template>

<script setup>
import { ref } from "vue";
import {
	Dialog,
	DialogPanel,
	Disclosure,
	DisclosureButton,
	DisclosurePanel,
	Popover,
	PopoverButton,
	PopoverGroup,
	PopoverPanel,
	RadioGroup,
	RadioGroupOption,
	Tab,
	TabGroup,
	TabList,
	TabPanel,
	TabPanels,
	TransitionChild,
	TransitionRoot,
} from "@headlessui/vue";
import {
	HeartIcon,
	MinusIcon,
	PlusIcon,
} from "@heroicons/vue/24/outline";
import { StarIcon } from "@heroicons/vue/20/solid";

const recipe = {
	name: "Classic Spaghetti Carbonara",
	cookTime: "30 minutes",
	servings: "4",
	rating: 5,
	images: [
		{
			id: 1,
			name: "Finished dish",
			src: "https://images.unsplash.com/photo-1612874742237-6526221588e3?h=1000&w=750&fit=crop",
			alt: "Plate of spaghetti carbonara with parmesan and black pepper",
		},
	],
	description: `
		<p>A traditional Roman pasta dish made with eggs, hard cheese, cured pork, and black pepper. Simple yet incredibly satisfying, this classic carbonara recipe creates a creamy sauce without using any cream!</p>
	`,
	ingredients: [
		"1 pound spaghetti",
		"4 oz guanciale or pancetta, diced",
		"4 large eggs",
		"1 cup freshly grated Pecorino Romano",
		"1 cup freshly grated Parmigiano-Reggiano",
		"2 tsp freshly ground black pepper",
		"Salt to taste"
	],
	instructions: {
		"Preparation": [
			"Bring a large pot of salted water to boil",
			"In a mixing bowl, whisk together eggs, grated cheese, and black pepper",
			"Cut guanciale into small cubes"
		],
		"Cooking": [
			"Cook pasta according to package directions until al dente",
			"While pasta cooks, sauté guanciale in a large pan until crispy",
			"Reserve 1 cup pasta water before draining",
			"Add hot pasta to pan with guanciale",
			"Remove from heat and quickly stir in egg mixture",
			"Add pasta water as needed for desired consistency"
		],
		"Serving": [
			"Serve immediately",
			"Top with additional grated cheese and black pepper",
			"Optionally garnish with fresh parsley"
		]
	}
};

const relatedRecipes = [
	{
		id: 1,
		name: "Spaghetti Aglio e Olio",
		cookTime: "15 minutes", 
		servings: "2",
		href: "#",
		imageSrc: "https://images.unsplash.com/photo-1551183053-bf91a1d81141?h=1000&w=750&fit=crop",
		imageAlt: "Bowl of spaghetti aglio e olio with garlic, olive oil and red pepper flakes",
	},
	{
		id: 2,
		name: "Fettuccine Alfredo",
		cookTime: "25 minutes",
		servings: "4", 
		href: "#",
		imageSrc: "https://images.unsplash.com/photo-1645112411341-6c4fd023714a?h=1000&w=750&fit=crop",
		imageAlt: "Creamy fettuccine alfredo pasta topped with parsley",
	},
	{
		id: 3,
		name: "Penne Arrabbiata",
		cookTime: "20 minutes",
		servings: "3",
		href: "#",
		imageSrc: "https://images.unsplash.com/photo-1563379926898-05f4575a45d8?h=1000&w=750&fit=crop", 
		imageAlt: "Spicy penne arrabbiata pasta in tomato sauce",
	},
];

</script>
