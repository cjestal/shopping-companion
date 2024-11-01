<template>
	<HomeRecipesSection />
	<HomePairingsSection />
	<HomeDepartmentsSection />

	<!-- Advertised Specials section -->
	<section
		aria-labelledby="category-heading"
		class="pt-24 sm:pt-32 xl:mx-auto xl:max-w-7xl xl:px-8"
	>
		<div
			class="px-4 sm:flex sm:items-center sm:justify-between sm:px-6 lg:px-8 xl:px-0"
		>
			<h2
				id="category-heading"
				class="text-2xl font-bold tracking-tight text-gray-900"
			>
				Advertised Specials
			</h2>
			<a
				href="#"
				class="hidden text-sm font-semibold text-red-600 hover:text-red-500 sm:block"
			>
				Browse all departments
				<span aria-hidden="true"> &rarr;</span>
			</a>
		</div>

		<div class="mt-4 flow-root">
			<div class="-my-2">
				<div
					class="relative box-content h-80 overflow-x-auto py-2 xl:overflow-visible"
				>
					<div
						class="absolute flex space-x-8 px-4 sm:px-6 lg:px-8 xl:relative xl:grid xl:grid-cols-5 xl:gap-x-8 xl:space-x-0 xl:px-0"
					>
						<a
							v-for="special in specials"
							:key="special.name"
							:href="special.href"
							class="relative flex h-80 w-56 flex-col overflow-hidden rounded-lg p-6 hover:opacity-75 xl:w-auto"
						>
							<span aria-hidden="true" class="absolute inset-0">
								<img
									:src="special.imageSrc"
									alt=""
									class="h-full w-full object-cover object-center"
								/>
							</span>
							<span
								aria-hidden="true"
								class="absolute inset-x-0 bottom-0 h-2/3 bg-gradient-to-t from-gray-800 opacity-50"
							/>
							<span
								class="relative mt-auto text-center text-xl font-bold text-white"
								>{{ special.name }}</span
							>
						</a>
					</div>
				</div>
			</div>
		</div>

		<div class="mt-6 px-4 sm:hidden">
			<a
				href="#"
				class="block text-sm font-semibold text-red-600 hover:text-red-500"
			>
				Browse all advertised specials
				<span aria-hidden="true"> &rarr;</span>
			</a>
		</div>
	</section>

</template>

<script setup>


const specials = [
	{
		name: "Organic Avocados",
		href: "#",
		imageSrc: "https://images.unsplash.com/photo-1523049673857-eb18f1d7b578",
		imageAlt: "Fresh ripe organic avocados.",
		description: "2 for $5 - Save $2! Perfect ripeness guaranteed.",
	},
	{
		name: "Fresh Atlantic Salmon",
		href: "#",
		imageSrc: "https://images.unsplash.com/photo-1580476262798-bddd9f4b7369",
		imageAlt: "Raw salmon fillet on ice.",
		description: "$12.99/lb - Save $4/lb! Wild-caught Atlantic salmon fillets.",
	},
	{
		name: "Whole Grain Bread",
		href: "#",
		imageSrc: "https://images.unsplash.com/photo-1509440159596-0249088772ff",
		imageAlt: "Freshly baked whole grain bread loaf.",
		description: "Buy 1 Get 1 Free! Freshly baked in-store daily.",
	},
	{
		name: "Organic Milk",
		href: "#",
		imageSrc: "https://images.unsplash.com/photo-1550583724-b2692b85b150",
		imageAlt: "Glass bottle of organic whole milk.",
		description: "$3.99/gallon - Save $1! Locally sourced organic milk.",
	},
	{
		name: "Fresh Strawberries",
		href: "#",
		imageSrc: "https://images.unsplash.com/photo-1518635017498-87f514b751ba",
		imageAlt: "Fresh red strawberries.",
		description: "2 pints for $5 - Save $3! Sweet and juicy local berries.",
	},
];
</script>
