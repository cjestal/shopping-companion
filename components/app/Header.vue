<template>
	<!-- Mobile menu -->
	<TransitionRoot as="template" :show="mobileMenuOpen">
		<Dialog class="relative z-40 lg:hidden" @close="mobileMenuOpen = false">
			<TransitionChild
				as="template"
				enter="transition-opacity ease-linear duration-300"
				enter-from="opacity-0"
				enter-to="opacity-100"
				leave="transition-opacity ease-linear duration-300"
				leave-from="opacity-100"
				leave-to="opacity-0"
			>
				<div class="fixed inset-0 bg-black bg-opacity-25" />
			</TransitionChild>

			<div class="fixed inset-0 z-40 flex">
				<TransitionChild
					as="template"
					enter="transition ease-in-out duration-300 transform"
					enter-from="-translate-x-full"
					enter-to="translate-x-0"
					leave="transition ease-in-out duration-300 transform"
					leave-from="translate-x-0"
					leave-to="-translate-x-full"
				>
					<DialogPanel
						class="relative flex w-full max-w-xs flex-col overflow-y-auto bg-white pb-12 shadow-xl"
					>
						<div class="flex px-4 pb-2 pt-5">
							<button
								type="button"
								class="-m-2 inline-flex items-center justify-center rounded-md p-2 text-gray-400"
								@click="mobileMenuOpen = false"
							>
								<span class="sr-only">Close menu</span>
								<XMarkIcon class="h-6 w-6" aria-hidden="true" />
							</button>
						</div>

						<!-- Links -->
						<TabGroup as="div" class="mt-2">
							<div class="border-b border-gray-200">
								<TabList class="-mb-px flex space-x-8 px-4">
									<Tab
										as="template"
										v-for="category in navigation.categories"
										:key="category.name"
										v-slot="{ selected }"
									>
										<button
											:class="[
												selected
													? 'border-red-800 text-red-800'
													: 'border-transparent text-gray-900',
												'flex-1 whitespace-nowrap border-b-2 px-1 py-4 text-base font-medium',
											]"
										>
											{{ category.name }}
										</button>
									</Tab>
								</TabList>
							</div>
							<TabPanels as="template">
								<TabPanel
									v-for="category in navigation.categories"
									:key="category.name"
									class="space-y-12 px-4 py-6"
								>
									<div class="grid grid-cols-2 gap-x-4 gap-y-10">
										<div
											v-for="item in category.featured"
											:key="item.name"
											class="group relative"
										>
											<div
												class="aspect-h-1 aspect-w-1 overflow-hidden rounded-md bg-gray-100 group-hover:opacity-75"
											>
												<img
													:src="item.imageSrc"
													:alt="item.imageAlt"
													class="object-cover object-center"
												/>
											</div>
											<a
												:href="item.href"
												class="mt-6 block text-sm font-medium text-gray-900"
											>
												<span
													class="absolute inset-0 z-10"
													aria-hidden="true"
												/>
												{{ item.name }}
											</a>
											<p aria-hidden="true" class="mt-1 text-sm text-gray-500">
												Shop now
											</p>
										</div>
									</div>
								</TabPanel>
							</TabPanels>
						</TabGroup>

						<div class="space-y-6 border-t border-gray-200 px-4 py-6">
							<div
								v-for="page in navigation.pages"
								:key="page.name"
								class="flow-root"
							>
								<a
									:href="page.href"
									class="-m-2 block p-2 font-medium text-gray-900"
									>{{ page.name }}</a
								>
							</div>
						</div>

						<div class="space-y-6 border-t border-gray-200 px-4 py-6">
							<div class="flow-root">
								<a href="#" class="-m-2 block p-2 font-medium text-gray-900"
									>Create an account</a
								>
							</div>
							<div class="flow-root">
								<a href="#" class="-m-2 block p-2 font-medium text-gray-900"
									>Sign in</a
								>
							</div>
						</div>
					</DialogPanel>
				</TransitionChild>
			</div>
		</Dialog>
	</TransitionRoot>

	<!-- Hero section -->
	<div class="relative bg-gray-900">
		<!-- Decorative image and overlay -->
		<div aria-hidden="true" class="absolute inset-0 overflow-hidden">
			<img
				src="https://images.unsplash.com/photo-1625631980741-33a7752108f4?auto=format&fit=crop&w=2000"
				alt=""
				class="h-full w-full object-cover object-center"
			/>
		</div>
		<div aria-hidden="true" class="absolute inset-0 bg-gray-900 opacity-50" />

		<!-- Navigation -->
		<header class="relative z-10">
			<nav aria-label="Top">
				<!-- Top navigation -->
				<div class="bg-red-800">
					<div
						class="mx-auto flex h-10 max-w-7xl items-center justify-end px-4 sm:px-6 lg:px-8"
					>
						<div class="flex items-center space-x-6">
							<a
								href="#"
								class="text-sm font-medium text-white hover:text-gray-100"
								>Sign in</a
							>
							<a
								href="#"
								class="text-sm font-medium text-white hover:text-gray-100"
								>Create an account</a
							>
						</div>
					</div>
				</div>

				<!-- Secondary navigation -->
				<div class="bg-white bg-opacity-10 backdrop-blur-md backdrop-filter">
					<div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
						<div>
							<div class="flex h-16 items-center justify-between">
								<!-- Logo (lg+) -->
								<div class="hidden lg:flex lg:flex-1 lg:items-center">
									<a href="#">
										<span class="sr-only">Your Company</span>
										<img
											class="h-8 w-auto"
											src="https://api.longos.com/medias/logo-widescreen.svg?context=bWFzdGVyfHJvb3R8ODQ3OXxpbWFnZS9zdmcreG1sfGFEbGlMMmd5TlM4NU5qRTJOakU1TnprNE5UVTRMMnh2WjI4dGQybGtaWE5qY21WbGJpNXpkbWN8OTIzZmNkMWY4ZjljNDkwZmE0YWJhNmNjZjY4ZjVhODM2ZDZhOTY5ZGQyMTUyNmQxYjE4ZTE3N2I3ZjZiNzAxNg"
											alt=""
										/>
									</a>
								</div>

								<div class="hidden h-full lg:flex">
									<!-- Flyout menus -->
									<PopoverGroup class="inset-x-0 bottom-0 px-4">
										<div class="flex h-full justify-center space-x-8">
											<Popover
												v-for="category in navigation.categories"
												:key="category.name"
												class="flex"
												v-slot="{ open }"
											>
												<div class="relative flex">
													<PopoverButton
														class="relative z-10 flex items-center justify-center text-sm font-medium text-white transition-colors duration-200 ease-out"
													>
														{{ category.name }}
														<span
															:class="[
																open ? 'bg-white' : '',
																'absolute inset-x-0 -bottom-px h-0.5 transition duration-200 ease-out',
															]"
															aria-hidden="true"
														/>
													</PopoverButton>
												</div>

												<transition
													enter-active-class="transition ease-out duration-200"
													enter-from-class="opacity-0"
													enter-to-class="opacity-100"
													leave-active-class="transition ease-in duration-150"
													leave-from-class="opacity-100"
													leave-to-class="opacity-0"
												>
													<PopoverPanel
														class="absolute inset-x-0 top-full text-sm text-gray-500"
													>
														<!-- Presentational element used to render the bottom shadow, if we put the shadow on the actual panel it pokes out the top, so we use this shorter element to hide the top of the shadow -->
														<div
															class="absolute inset-0 top-1/2 bg-white shadow"
															aria-hidden="true"
														/>

														<div class="relative bg-white">
															<div
																class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8"
															>
																<div
																	class="grid grid-cols-4 gap-x-8 gap-y-10 py-16"
																>
																	<div
																		v-for="item in category.featured"
																		:key="item.name"
																		class="group relative"
																	>
																		<div
																			class="aspect-h-1 aspect-w-1 overflow-hidden rounded-md bg-gray-100 group-hover:opacity-75"
																		>
																			<img
																				:src="item.imageSrc"
																				:alt="item.imageAlt"
																				class="object-cover object-center"
																			/>
																		</div>
																		<a
																			:href="item.href"
																			class="mt-4 block font-medium text-gray-900"
																		>
																			<span
																				class="absolute inset-0 z-10"
																				aria-hidden="true"
																			/>
																			{{ item.name }}
																		</a>
																		<p aria-hidden="true" class="mt-1">
																			Shop now
																		</p>
																	</div>
																</div>
															</div>
														</div>
													</PopoverPanel>
												</transition>
											</Popover>

											<a
												v-for="page in navigation.pages"
												:key="page.name"
												:href="page.href"
												class="flex items-center text-sm font-medium text-white"
												>{{ page.name }}</a
											>
										</div>
									</PopoverGroup>
								</div>

								<!-- Mobile menu and search (lg-) -->
								<div class="flex flex-1 items-center lg:hidden">
									<button
										type="button"
										class="-ml-2 p-2 text-white"
										@click="mobileMenuOpen = true"
									>
										<span class="sr-only">Open menu</span>
										<Bars3Icon class="h-6 w-6" aria-hidden="true" />
									</button>

									<!-- Search -->
									<a href="#" class="ml-2 p-2 text-white">
										<span class="sr-only">Search</span>
										<MagnifyingGlassIcon class="h-6 w-6" aria-hidden="true" />
									</a>
								</div>

								<!-- Logo (lg-) -->
								<a href="#" class="lg:hidden">
									<span class="sr-only">Your Company</span>
									<img
										src="https://api.longos.com/medias/logo-widescreen.svg?context=bWFzdGVyfHJvb3R8ODQ3OXxpbWFnZS9zdmcreG1sfGFEbGlMMmd5TlM4NU5qRTJOakU1TnprNE5UVTRMMnh2WjI4dGQybGtaWE5qY21WbGJpNXpkbWN8OTIzZmNkMWY4ZjljNDkwZmE0YWJhNmNjZjY4ZjVhODM2ZDZhOTY5ZGQyMTUyNmQxYjE4ZTE3N2I3ZjZiNzAxNg"
										alt=""
										class="h-8 w-auto"
									/>
								</a>

								<div class="flex flex-1 items-center justify-end">
									<a
										href="#"
										class="hidden text-sm font-medium text-white lg:block"
										>Search</a
									>

									<div class="flex items-center lg:ml-8">
										<!-- QR Code Scanner -->
										<div class="flow-root mr-4">
											<button
												@click="open = !open"
												class="group -m-2 flex items-center p-2"
											>
												<QrCodeIcon
													class="h-6 w-6 flex-shrink-0 text-white"
													aria-hidden="true"
												/>
												<span class="sr-only">Open QR code scanner</span>
											</button>
										</div>

										<!-- Cart -->
										<div class="flow-root" @click="shoppingListOpen = true">
											<a href="#" class="group -m-2 flex items-center p-2">
												<ShoppingBagIcon
													class="h-6 w-6 flex-shrink-0 text-white"
													aria-hidden="true"
												/>
												<span class="ml-2 text-sm font-medium text-white"
													>0</span
												>
												<span class="sr-only">items in cart, view bag</span>
											</a>
										</div>
									</div>
								</div>
							</div>
						</div>
					</div>
				</div>
			</nav>
		</header>

		<div
			class="relative mx-auto flex max-w-3xl flex-col items-center px-6 py-32 text-center sm:py-64 lg:px-0"
		>
			<h1 class="text-4xl font-bold tracking-tight text-white lg:text-6xl">
				Scan to Get Started
			</h1>
			<p class="mt-4 text-xl text-white">
				Simply scan any product's QR code to instantly see recipes and other
				products to pair with. Get started by scanning your first item.
			</p>
			<a
				href="#"
				class="mt-8 inline-block rounded-md border border-transparent bg-white px-8 py-3 text-base font-medium text-gray-900 hover:bg-gray-100"
				>Scan QR Code</a
			>
		</div>
	</div>

	<!-- QR Code Panel -->
	<TransitionRoot as="template" :show="open">
		<Dialog class="relative z-10" @close="open = false">
			<div class="fixed inset-0" />

			<div class="fixed inset-0 overflow-hidden">
				<div class="absolute inset-0 overflow-hidden">
					<div
						class="pointer-events-none fixed inset-y-0 right-0 flex max-w-full pl-10"
					>
						<TransitionChild
							as="template"
							enter="transform transition ease-in-out duration-500 sm:duration-800"
							enter-from="translate-x-full"
							enter-to="translate-x-0"
							leave="transform transition ease-in-out duration-500 sm:duration-800"
							leave-from="translate-x-0"
							leave-to="translate-x-full"
						>
							<DialogPanel class="pointer-events-auto w-screen max-w-md">
								<div
									class="flex h-full flex-col overflow-y-scroll bg-white shadow-xl"
								>
									<div class="bg-red-700 px-4 py-6 sm:px-6">
										<div class="flex items-center justify-between">
											<DialogTitle class="text-base font-semibold text-white"
												>Scan QR Code</DialogTitle
											>
											<div class="ml-3 flex h-7 items-center">
												<button
													type="button"
													class="relative rounded-md bg-red-800 text-red-200 hover:text-white focus:outline-none focus:ring-2 focus:ring-white"
													@click="open = false"
												>
													<span class="absolute -inset-2.5" />
													<span class="sr-only">Close panel</span>
													<XMarkIcon class="h-6 w-6" aria-hidden="true" />
												</button>
											</div>
										</div>
										<div class="mt-1">
											<p class="text-sm text-red-300">
												Position the code within the scanner frame.
											</p>
										</div>
									</div>

									<!-- Fake Scanner -->
									<div class="relative flex-1 px-4 py-6 sm:px-6">
										<div
											class="relative mx-auto w-full max-w-sm overflow-hidden rounded-lg bg-gray-100"
										>
											<div class="aspect-w-1 aspect-h-1">
												<div
													class="absolute inset-0 flex items-center justify-center"
												>
													<div
														class="h-48 w-48 rounded-lg border-2 border-dashed border-gray-400"
													></div>
												</div>
												<img
													src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"
													class="h-full w-full object-cover"
													alt="QR Scanner View"
												/>
											</div>
											<div
												class="absolute inset-0 bg-gradient-to-t from-gray-800 via-transparent"
											></div>
										</div>
									</div>

									<!-- fillers -->
									<!-- Recent Scans -->
									<div class="px-4 py-4 sm:px-6">
										<h3 class="text-sm font-medium text-gray-900">
											Recent Scans
										</h3>
										<div class="mt-2 flow-root">
											<div class="flex flex-col space-y-2">
												<div
													class="flex items-center justify-between rounded-lg bg-gray-50 p-4"
												>
													<div class="flex items-center">
														<div class="h-10 w-10 flex-shrink-0">
															<img
																src="https://tailwindui.com/img/ecommerce-images/product-page-01-related-product-01.jpg"
																alt=""
																class="h-full w-full rounded-lg object-cover"
															/>
														</div>
														<div class="ml-4">
															<p class="text-sm font-medium text-gray-900">
																Organic Bananas
															</p>
															<p class="text-sm text-gray-500">
																Scanned 2 minutes ago
															</p>
														</div>
													</div>
													<button
														type="button"
														class="rounded-md bg-white px-2.5 py-1.5 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50"
													>
														View
													</button>
												</div>

												<div
													class="flex items-center justify-between rounded-lg bg-gray-50 p-4"
												>
													<div class="flex items-center">
														<div class="h-10 w-10 flex-shrink-0">
															<img
																src="https://tailwindui.com/img/ecommerce-images/product-page-01-related-product-02.jpg"
																alt=""
																class="h-full w-full rounded-lg object-cover"
															/>
														</div>
														<div class="ml-4">
															<p class="text-sm font-medium text-gray-900">
																Fresh Strawberries
															</p>
															<p class="text-sm text-gray-500">
																Scanned 15 minutes ago
															</p>
														</div>
													</div>
													<button
														type="button"
														class="rounded-md bg-white px-2.5 py-1.5 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50"
													>
														View
													</button>
												</div>
											</div>
										</div>
									</div>

									<!-- Help Text -->
									<div class="px-4 pb-6 sm:px-6">
										<div class="rounded-md bg-blue-50 p-4">
											<div class="flex">
												<div class="flex-shrink-0">
													<QuestionMarkCircleIcon
														class="h-5 w-5 text-blue-400"
														aria-hidden="true"
													/>
												</div>
												<div class="ml-3">
													<h3 class="text-sm font-medium text-blue-800">
														Need Help?
													</h3>
													<div class="mt-2 text-sm text-blue-800">
														<p>Having trouble scanning? Make sure:</p>
														<ul class="list-disc pl-5 space-y-1 mt-2">
															<li>The QR code is well-lit</li>
															<li>Your camera lens is clean</li>
															<li>The code is centered in the frame</li>
														</ul>
													</div>
												</div>
											</div>
										</div>
									</div>
								</div>
							</DialogPanel>
						</TransitionChild>
					</div>
				</div>
			</div>
		</Dialog>
	</TransitionRoot>

	<!-- Shopping List Panel -->
	<TransitionRoot as="template" :show="shoppingListOpen">
		<Dialog as="div" class="relative z-10" @close="shoppingListOpen = false">
			<div class="fixed inset-0" />

			<div class="fixed inset-0 overflow-hidden">
				<div class="absolute inset-0 overflow-hidden">
					<div
						class="pointer-events-none fixed inset-y-0 right-0 flex max-w-full pl-10"
					>
						<TransitionChild
							as="template"
							enter="transform transition ease-in-out duration-500 sm:duration-800"
							enter-from="translate-x-full"
							enter-to="translate-x-0"
							leave="transform transition ease-in-out duration-500 sm:duration-800"
							leave-from="translate-x-0"
							leave-to="translate-x-full"
						>
							<DialogPanel class="pointer-events-auto w-screen max-w-md">
								<div
									class="flex h-full flex-col overflow-y-scroll bg-white shadow-xl"
								>
									<div class="bg-red-700 px-4 py-6 sm:px-6">
										<div class="flex items-center justify-between">
											<DialogTitle class="text-base font-semibold text-white"
												>Shopping List</DialogTitle
											>
											<div class="ml-3 flex h-7 items-center">
												<button
													type="button"
													class="relative rounded-md bg-red-800 text-red-200 hover:text-white focus:outline-none focus:ring-2 focus:ring-white"
													@click="shoppingListOpen = false"
												>
													<span class="absolute -inset-2.5" />
													<span class="sr-only">Close panel</span>
													<XMarkIcon class="h-6 w-6" aria-hidden="true" />
												</button>
											</div>
										</div>
										<div class="mt-1">
											<p class="text-sm text-red-300">
												Your shopping list items
											</p>
										</div>
									</div>

									<div class="flex-1 overflow-y-auto px-4 py-6 sm:px-6">
										<div class="flow-root">
											<div class="space-y-6">
												<fieldset v-for="recipe in shoppingList" :key="recipe.name">
													<legend class="text-lg font-bold text-gray-900 border-b-2 border-red-600 pb-1 inline-block">
														{{ recipe.name }}
													</legend>
													<div
														class="mt-4 divide-y divide-gray-200 border-b border-t border-gray-200"
													>
														<div
															v-for="(ingredient, idx) in recipe.ingredients"
															:key="idx"
															class="relative flex items-start py-4 cursor-pointer"
															@click="recipe.selected[idx] = !recipe.selected[idx]"
														>
															<div class="min-w-0 flex-1 text-sm/6">
																<label
																	:for="`${recipe.id}-${idx}`"
																	class="select-none font-medium"
																	:class="{
																		'text-gray-900': !recipe.selected[idx],
																		'text-gray-500 line-through': recipe.selected[idx]
																	}"
																	>{{ ingredient }}</label
																>
															</div>
															<div class="ml-3 flex h-6 items-center">
																<input
																	:id="`${recipe.id}-${idx}`"
																	:name="`${recipe.id}-${idx}`"
																	type="checkbox"
																	v-model="recipe.selected[idx]"
																	class="h-4 w-4 rounded border-gray-300 text-red-600 focus:ring-red-600"
																	@click.stop
																/>
															</div>
														</div>
													</div>
												</fieldset>
											</div>
										</div>
									</div>

									<div class="border-t border-gray-200 px-4 py-6 sm:px-6">
										<div
											class="flex justify-between text-base font-medium text-gray-900"
										>
											<p>Items Selected</p>
											<p>{{ selectedCount }} of {{ totalItems }}</p>
										</div>
										<p class="mt-0.5 text-sm text-gray-500">
											Check off items as you add them to your cart
										</p>
										<div class="mt-6">
											<button
												type="button"
												@click="shoppingList.forEach(recipe => recipe.selected = recipe.selected.map(() => true))"
												class="flex items-center justify-center rounded-md border border-transparent bg-red-600 px-6 py-3 text-base font-medium text-white shadow-sm hover:bg-red-700 w-full"
											>
												Add all items to cart
											</button>
										</div>
										<div
											class="mt-6 flex justify-center text-center text-sm text-gray-500"
										>
											<p>
												or
												<button
													type="button"
													class="font-medium text-red-600 hover:text-red-500"
													@click="clearSelections"
												>
													Clear All Selections
													<span aria-hidden="true"> &times;</span>
												</button>
											</p>
										</div>
									</div>
								</div>
							</DialogPanel>
						</TransitionChild>
					</div>
				</div>
			</div>
		</Dialog>
	</TransitionRoot>
</template>

<script setup>
import { ref, computed } from "vue";

import {
	Dialog,
	DialogPanel,
	DialogTitle,
	Popover,
	PopoverButton,
	PopoverGroup,
	PopoverPanel,
	Tab,
	TabGroup,
	TabList,
	TabPanel,
	TabPanels,
	TransitionChild,
	TransitionRoot,
} from "@headlessui/vue";
import {
	Bars3Icon,
	MagnifyingGlassIcon,
	QuestionMarkCircleIcon,
	XMarkIcon,
	ShoppingBagIcon,
	QrCodeIcon,
} from "@heroicons/vue/24/outline";
import { ChevronDownIcon } from "@heroicons/vue/20/solid";

const mobileMenuOpen = ref(false);
const open = ref(false);
const shoppingListOpen = ref(false);

const shoppingList = ref([
	{
		id: 'banana-bread',
		name: 'Banana Bread',
		ingredients: ['Bananas', 'Flour', 'Sugar', 'Eggs'],
		selected: [false, false, false, false]
	},
	{
		id: 'smoothie',
		name: 'Strawberry Smoothie', 
		ingredients: ['Strawberries', 'Yogurt', 'Honey', 'Ice'],
		selected: [false, false, false, false]
	},
	{
		id: 'chicken-stir-fry',
		name: 'Chicken Stir Fry',
		ingredients: ['Chicken Breast', 'Bell Peppers', 'Broccoli', 'Soy Sauce', 'Rice'],
		selected: [false, false, false, false, false]
	},
	{
		id: 'chocolate-chip-cookies',
		name: 'Chocolate Chip Cookies',
		ingredients: ['Butter', 'Brown Sugar', 'Flour', 'Chocolate Chips', 'Vanilla Extract'],
		selected: [false, false, false, false, false]
	}
]);

const selectedCount = computed(() => {
	return shoppingList.value.reduce((total, recipe) => {
		return total + recipe.selected.filter(Boolean).length;
	}, 0);
});

const totalItems = computed(() => {
	return shoppingList.value.reduce((total, recipe) => {
		return total + recipe.ingredients.length;
	}, 0);
});

const clearSelections = () => {
	shoppingList.value.forEach(recipe => {
		recipe.selected = recipe.selected.map(() => false);
	});
};

const navigation = {
	categories: [
		{
			name: "Products",
			featured: [
				{
					name: "Advertised Specials",
					href: "#",
					imageSrc:
						"https://tailwindui.com/plus/img/ecommerce-images/mega-menu-category-01.jpg",
					imageAlt:
						"Models sitting back to back, wearing Basic Tee in black and bone.",
				},
				{
					name: "Popular Recipes",
					href: "#",
					imageSrc:
						"https://tailwindui.com/plus/img/ecommerce-images/mega-menu-category-02.jpg",
					imageAlt:
						"Close up of Basic Tee fall bundle with off-white, ochre, olive, and black tees.",
				},
				{
					name: "Accessories",
					href: "#",
					imageSrc:
						"https://tailwindui.com/plus/img/ecommerce-images/mega-menu-category-03.jpg",
					imageAlt:
						"Model wearing minimalist watch with black wristband and white watch face.",
				},
				{
					name: "Carry",
					href: "#",
					imageSrc:
						"https://tailwindui.com/plus/img/ecommerce-images/mega-menu-category-04.jpg",
					imageAlt:
						"Model opening tan leather long wallet with credit card pockets and cash pouch.",
				},
			],
		},
		{
			name: "Recipes",
			featured: [
				{
					name: "Quick & Easy",
					href: "#",
					imageSrc:
						"https://images.unsplash.com/photo-1490645935967-10de6ba17061?h=400&fit=crop",
					imageAlt: "Bowl of fresh salad with grilled chicken and vegetables.",
				},
				{
					name: "Healthy Options",
					href: "#",
					imageSrc:
						"https://images.unsplash.com/photo-1546069901-ba9599a7e63c?h=400&fit=crop",
					imageAlt: "Colorful buddha bowl with quinoa, vegetables and tofu.",
				},
				{
					name: "Family Favorites",
					href: "#",
					imageSrc:
						"https://images.unsplash.com/photo-1504674900247-0877df9cc836?h=400&fit=crop",
					imageAlt:
						"Large family style pasta dish with garlic bread on rustic wooden table.",
				},
				{
					name: "Seasonal Specials",
					href: "#",
					imageSrc:
						"https://images.unsplash.com/photo-1511690743698-d9d85f2fbf38?h=400&fit=crop",
					imageAlt: "Autumn harvest soup with fresh bread and herbs.",
				},
			],
		},
	],
	pages: [
		{ name: "Company", href: "#" },
		{ name: "Stores", href: "#" },
	],
};
</script>
