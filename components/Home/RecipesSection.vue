<template>
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
				Recipes
			</h2>
			<NuxtLink
				to="/recipe"
				class="hidden text-sm font-semibold text-red-600 hover:text-red-500 sm:block"
			>
				Browse all recipes
				<span aria-hidden="true"> &rarr;</span>
			</NuxtLink>
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
							v-for="recipe in recipes"
							:key="recipe.name"
							:href="recipe.href"
							class="relative flex h-80 w-56 flex-col overflow-hidden rounded-lg p-6 hover:opacity-75 xl:w-auto"
						>
							<span aria-hidden="true" class="absolute inset-0">
								<img
									:src="recipe.imageSrc"
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
								>{{ recipe.name }}</span
							>
						</a>
					</div>
				</div>
			</div>
		</div>

		<div class="mt-6 px-4 sm:hidden">
			<NuxtLink
				to="/recipe"
				class="block text-sm font-semibold text-red-600 hover:text-red-500"
			>
				Browse all recipes
				<span aria-hidden="true"> &rarr;</span>
			</NuxtLink>
		</div>
	</section>
</template>

<script setup>
const recipes = [
	{
		name: "Quick & Easy",
		href: "#",
		imageSrc:
			"https://images.unsplash.com/photo-1490645935967-10de6ba17061?h=400&fit=crop",
	},
	{
		name: "Healthy Options",
		href: "#",
		imageSrc:
			"https://images.unsplash.com/photo-1546069901-ba9599a7e63c?h=400&fit=crop",
	},
	{
		name: "Family Favorites",
		href: "#",
		imageSrc:
			"https://images.unsplash.com/photo-1504674900247-0877df9cc836?h=400&fit=crop",
	},
	{
		name: "Seasonal Specials",
		href: "#",
		imageSrc:
			"https://images.unsplash.com/photo-1511690743698-d9d85f2fbf38?h=400&fit=crop",
	},
	{
		name: "Popular Recipes",
		href: "#",
		imageSrc:
			"https://images.unsplash.com/photo-1495521821757-a1efb6729352?h=400&fit=crop",
	},
];
</script>
