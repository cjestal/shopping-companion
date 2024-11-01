<template>
	<div class="bg-white">
		<AppHeader />

		<main>
			<NuxtPage />
		</main>
		<AppFooter />
	</div>
</template>

<script setup>
import { ref } from "vue";



const mobileMenuOpen = ref(false);
</script>
