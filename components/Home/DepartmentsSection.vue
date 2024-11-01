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
				Shop by Department
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
							v-for="category in categories"
							:key="category.name"
							:href="category.href"
							class="relative flex h-80 w-56 flex-col overflow-hidden rounded-lg p-6 hover:opacity-75 xl:w-auto"
						>
							<span aria-hidden="true" class="absolute inset-0">
								<img
									:src="category.imageSrc"
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
								>{{ category.name }}</span
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
				Browse all categories
				<span aria-hidden="true"> &rarr;</span>
			</a>
		</div>
	</section>
</template>

<script setup>
const categories = [
	{
		name: "Produce",
		href: "#",
		imageSrc:
			"https://images.unsplash.com/photo-1610348725531-843dff563e2c?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80",
	},
	{
		name: "Meat & Seafood",
		href: "#",
		imageSrc:
			"https://images.unsplash.com/photo-1607623814075-e51df1bdc82f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80",
	},
	{
		name: "Bakery",
		href: "#",
		imageSrc:
			"https://images.unsplash.com/photo-1608198093002-ad4e005484ec?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1332&q=80",
	},
	{
		name: "Dairy & Eggs",
		href: "#",
		imageSrc:
			"https://images.unsplash.com/photo-1628088062854-d1870b4553da?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80",
	},
	{
		name: "Pantry",
		href: "#",
		imageSrc:
			"https://images.unsplash.com/photo-1584473457406-6240486418e9?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80",
	},
];
</script>
