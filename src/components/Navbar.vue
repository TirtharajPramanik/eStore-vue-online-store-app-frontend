<template>
	<nav class="py-4 px-4 flex max-w-xl mx-auto">
		<h3 class="text-3xl flex-auto">{{ navHeader }}</h3>
		<BellIcon class="w-6 h-6 mr-5" />
		<MenuAlt1Icon class="w-6 h-6" />
		<!-- <menu type="toolbar"></menu> -->
	</nav>
</template>

<script lang="ts">
import { BellIcon, MenuAlt1Icon } from '@heroicons/vue/outline';
export default {
	props: ['navHeader'],
	components: { BellIcon, MenuAlt1Icon },
};
</script>
