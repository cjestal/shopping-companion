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
				Popular Pairings
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
							v-for="pair in pairs"
							:key="pair.name"
							:href="pair.href"
							class="relative flex h-80 w-56 flex-col overflow-hidden rounded-lg p-6 hover:opacity-75 xl:w-auto"
						>
							<span aria-hidden="true" class="absolute inset-0">
								<img
									:src="pair.imageSrc"
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
								>{{ pair.name }}</span
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
				Browse all pairings
				<span aria-hidden="true"> &rarr;</span>
			</a>
		</div>
	</section>
</template>

<script setup>
const pairs = [
	{
		name: "Fresh Berries & Cream",
		href: "#",
		imageSrc:
			"https://images.unsplash.com/photo-1563746098251-d35aef196e83?ixlib=rb-4.0.3&auto=format&fit=crop&w=1170&q=80",
	},
	{
		name: "Steak & Wine",
		href: "#",
		imageSrc:
			"https://images.unsplash.com/photo-1544025162-d76694265947?ixlib=rb-4.0.3&auto=format&fit=crop&w=1170&q=80",
	},
	{
		name: "Cheese & Crackers",
		href: "#",
		imageSrc:
			"https://images.unsplash.com/photo-1625176978650-8fe14550b78d?ixlib=rb-4.0.3&auto=format&fit=crop&w=1332&q=80",
	},
	{
		name: "Coffee & Pastries",
		href: "#",
		imageSrc:
			"https://images.unsplash.com/photo-1495474472287-4d71bcdd2085?ixlib=rb-4.0.3&auto=format&fit=crop&w=1170&q=80",
	},
	{
		name: "Chips & Dip",
		href: "#",
		imageSrc:
			"https://images.unsplash.com/photo-1566478989037-eec170784d0b?ixlib=rb-4.0.3&auto=format&fit=crop&w=1170&q=80",
	},
];
</script>
